package com.example.kafka.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

import com.example.kafka.service.KafkaService;




@RestController
public class KafkaController {

    @Autowired
    private KafkaService kafkaService;

    @PostMapping("/sendMessageToKafkaWithKey")
    public ResponseEntity<String> publishMessageToKafka(@RequestBody String msg) {
        try {
            kafkaService.processMessage(msg);
            return new ResponseEntity<>("Send Successful", HttpStatus.OK);
        } catch (IllegalArgumentException e) {
            return new ResponseEntity<>(e.getMessage(), HttpStatus.BAD_REQUEST);
        } catch (Exception e) {
            return new ResponseEntity<>("Failed to send message: " + e.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
        }
    }
}

package com.example.kafka.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.stereotype.Component;

@Component
public class KafkaProducer {

	@Autowired
	private KafkaTemplate<String, String> kafkaTemplate;

	public void sendMessageToKafkaWithTopic(String selectedTopic, String msg) {
		kafkaTemplate.send(selectedTopic, msg);

	}

}

package com.example.kafka.service;

import org.json.JSONObject;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.example.kafka.RequestTypeEnum;



@Service
public class KafkaService {

    @Autowired
    private KafkaProducer producer;

    public void processMessage(String msg) {
        JSONObject inputPayload = new JSONObject(msg);
        String requestTypeValue = inputPayload.optString("RequestType");
        String topicName = inputPayload.optString("topic_name");

        if (!requestTypeValue.isEmpty()) {
        	RequestTypeEnum requestTypeEnum = RequestTypeEnum.fromValue(requestTypeValue);
            String selectedTopic = getTopicForRequestType(requestTypeEnum);
            if (selectedTopic != null) {
                producer.sendMessageToKafkaWithTopic(selectedTopic, msg);
                return;
            }
        }

        // If request_type is not provided or not recognized, use the topic_name
        if (!topicName.isEmpty()) {
            producer.sendMessageToKafkaWithTopic(topicName, msg);
            return;
        }

        throw new IllegalArgumentException("Either RequestType or topic_name must be provided");
    }

    private String getTopicForRequestType(RequestTypeEnum requestTypeEnum) {
        switch (requestTypeEnum) {
            case one:
                return "demo";
            case two:
                return "test-topic";
            case three:
                return "testkafka";
            default:
                return null;
        }
    }
}

package com.example.kafka;

public enum RequestTypeEnum {
    one,
    two,
    three;

    public static RequestTypeEnum fromValue(String value) {
        for (RequestTypeEnum type : values()) {
            if (type.name().equalsIgnoreCase(value)) {
                return type;
            }
        }
        throw new IllegalArgumentException("Invalid RequestType: " + value);
    }
}
