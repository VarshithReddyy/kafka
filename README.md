<?xml version="1.0" encoding="UTF-8"?>
<bpmn:definitions xmlns:bpmn="http://www.omg.org/spec/BPMN/20100524/MODEL" xmlns:bpmndi="http://www.omg.org/spec/BPMN/20100524/DI" xmlns:dc="http://www.omg.org/spec/DD/20100524/DC" xmlns:zeebe="http://camunda.org/schema/zeebe/1.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:bioc="http://bpmn.io/schema/bpmn/biocolor/1.0" xmlns:color="http://www.omg.org/spec/BPMN/non-normative/color/1.0" xmlns:di="http://www.omg.org/spec/DD/20100524/DI" xmlns:modeler="http://camunda.org/schema/modeler/1.0" id="Definitions_02omzwv" targetNamespace="http://bpmn.io/schema/bpmn" exporter="Camunda Modeler" exporterVersion="5.22.0" modeler:executionPlatform="Camunda Cloud" modeler:executionPlatformVersion="8.2.0">
  <bpmn:collaboration id="Collaboration_01ohlww">
    <bpmn:participant id="Participant_01ldumh" processRef="NAOProcess" />
    <bpmn:textAnnotation id="TextAnnotation_0n814vb">
      <bpmn:text>Replacement to SOR APIs</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:textAnnotation id="TextAnnotation_1n58fkh">
      <bpmn:text>RDM API replaces DCTM Kafka</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:textAnnotation id="TextAnnotation_0vocrsv">
      <bpmn:text>This message catch event get BOT update from BOPM backend service that intern consume message from BOT response TOPIC</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:textAnnotation id="TextAnnotation_1rsmd3f">
      <bpmn:text>Intern Task Router takes care of  Rule validation &amp; User Task Assignment</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:textAnnotation id="TextAnnotation_01dztd0">
      <bpmn:text>Intern Task Router takes care of Queue Assignment</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:textAnnotation id="TextAnnotation_1po6hnl">
      <bpmn:text>TOPIC: aws.src.bopm.notification.secure.bo-publish-bot</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:textAnnotation id="TextAnnotation_0jblcdl">
      <bpmn:text>1. Review history should be updated ()</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:textAnnotation id="TextAnnotation_0y0fy0b">
      <bpmn:text>DONE/HOLD</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:association id="Association_03ix82b" associationDirection="None" sourceRef="Flow_0lmnbph" targetRef="TextAnnotation_0y0fy0b" />
    <bpmn:textAnnotation id="TextAnnotation_04uaz4w">
      <bpmn:text>1. Log into change history 2. Status will be "DONE"          3. Call RDM API</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:association id="Association_1ism3za" associationDirection="None" sourceRef="Flow_167y00y" targetRef="TextAnnotation_04uaz4w" />
    <bpmn:textAnnotation id="TextAnnotation_0n1ta3o">
      <bpmn:text>DCTM call has been removed and just change history needs to be added.</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:textAnnotation id="TextAnnotation_1dpnhxg">
      <bpmn:text>IGO/NIGO</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:association id="Association_13lumkf" associationDirection="None" sourceRef="Flow_1vvedca" targetRef="TextAnnotation_1dpnhxg" />
    <bpmn:textAnnotation id="TextAnnotation_14n4h53">
      <bpmn:text>DCTM API data get refreshed every 5 mins so we need to make a call before secondary routing</bpmn:text>
    </bpmn:textAnnotation>
    <bpmn:association id="Association_091rpvg" associationDirection="None" sourceRef="Activity_0pq5ibg" targetRef="TextAnnotation_0n814vb" />
    <bpmn:association id="Association_0syytw4" associationDirection="None" sourceRef="Activity_1jxn3p2" targetRef="TextAnnotation_1rsmd3f" />
    <bpmn:association id="Association_1xwtn2y" associationDirection="None" sourceRef="Activity_1b3t5ut" targetRef="TextAnnotation_0n1ta3o" />
    <bpmn:association id="Association_06u1xqp" associationDirection="None" sourceRef="Activity_07vkhur" targetRef="TextAnnotation_1po6hnl" />
    <bpmn:association id="Association_1dh6g8i" associationDirection="None" sourceRef="Activity_0cwmd8n" targetRef="TextAnnotation_01dztd0" />
    <bpmn:association id="Association_017keau" associationDirection="None" sourceRef="Event_1wb5nu1" targetRef="TextAnnotation_0vocrsv" />
    <bpmn:association id="Association_1qfcwh0" associationDirection="None" sourceRef="Activity_1mjo9h7" targetRef="TextAnnotation_1n58fkh" />
  </bpmn:collaboration>
  <bpmn:process id="NAOProcess" name="NAOProcess" isExecutable="true">
    <bpmn:laneSet id="LaneSet_0p3wnik">
      <bpmn:lane id="Lane_0492jwa" name="BOT">
        <bpmn:flowNodeRef>Activity_07vkhur</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Event_1wb5nu1</bpmn:flowNodeRef>
      </bpmn:lane>
      <bpmn:lane id="Lane_1lio5cz" name="RDM\DCTM">
        <bpmn:flowNodeRef>Activity_1mjo9h7</bpmn:flowNodeRef>
      </bpmn:lane>
      <bpmn:lane id="Lane_0xx3o0a" name="BOPM">
        <bpmn:flowNodeRef>Activity_0b2ramb</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>StartEvent_1</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Activity_0pq5ibg</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Activity_1jxn3p2</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Gateway_0ujr21r</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Gateway_1m0d8gl</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Activity_0ahc8wh</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Activity_1b3t5ut</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Gateway_1x2uyvd</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Event_0f9xpwo</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Activity_0jo75v6</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Activity_1m11o8u</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Activity_14sj7kt</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Activity_0cwmd8n</bpmn:flowNodeRef>
        <bpmn:flowNodeRef>Activity_1byn9g1</bpmn:flowNodeRef>
      </bpmn:lane>
    </bpmn:laneSet>
    <bpmn:serviceTask id="Activity_0b2ramb" name="Log NAO Process">
      <bpmn:extensionElements>
        <zeebe:taskDefinition type="nao-process-logProcessData" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_0mm47u4</bpmn:incoming>
      <bpmn:outgoing>Flow_1vfcao6</bpmn:outgoing>
    </bpmn:serviceTask>
    <bpmn:startEvent id="StartEvent_1">
      <bpmn:outgoing>Flow_0mm47u4</bpmn:outgoing>
    </bpmn:startEvent>
    <bpmn:serviceTask id="Activity_0pq5ibg" name="Call Account DCTM API Worker">
      <bpmn:extensionElements>
        <zeebe:taskDefinition type="nao-process-callDCTMAPIBeforePrimeRule" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_1vfcao6</bpmn:incoming>
      <bpmn:outgoing>Flow_0sgm0h0</bpmn:outgoing>
    </bpmn:serviceTask>
    <bpmn:callActivity id="Activity_1jxn3p2" name="Call  Primary Task Router">
      <bpmn:extensionElements>
        <zeebe:calledElement processId="bopm-task-router" propagateAllChildVariables="true" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_0q0mi23</bpmn:incoming>
      <bpmn:incoming>Flow_0sgm0h0</bpmn:incoming>
      <bpmn:outgoing>Flow_1ipzeyu</bpmn:outgoing>
    </bpmn:callActivity>
    <bpmn:sequenceFlow id="Flow_0mm47u4" sourceRef="StartEvent_1" targetRef="Activity_0b2ramb" />
    <bpmn:sequenceFlow id="Flow_1vfcao6" sourceRef="Activity_0b2ramb" targetRef="Activity_0pq5ibg" />
    <bpmn:sequenceFlow id="Flow_0sgm0h0" sourceRef="Activity_0pq5ibg" targetRef="Activity_1jxn3p2" />
    <bpmn:sequenceFlow id="Flow_0lmnbph" sourceRef="Gateway_0ujr21r" targetRef="Gateway_1m0d8gl">
      <bpmn:conditionExpression xsi:type="bpmn:tFormalExpression">=(isDecision != null and isDecision = "HOLD") or
(isDecision != null and isDecision = "DONE")</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:sequenceFlow id="Flow_1ovgttr" name="Manual / Rule Output status = Robotic" sourceRef="Gateway_0ujr21r" targetRef="Activity_1b3t5ut">
      <bpmn:conditionExpression xsi:type="bpmn:tFormalExpression">=(isDecision != null and isDecision = "Robotics")</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:sequenceFlow id="Flow_1vvedca" sourceRef="Gateway_0ujr21r" targetRef="Activity_14sj7kt">
      <bpmn:conditionExpression xsi:type="bpmn:tFormalExpression">=(isDecision != null and isDecision != "IGO") or (isDecision != null and isDecision != "NIGO")</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:sequenceFlow id="Flow_167y00y" sourceRef="Activity_0cwmd8n" targetRef="Gateway_1m0d8gl" />
    <bpmn:sequenceFlow id="Flow_15xh55c" name="OpsReview=DONE" sourceRef="Gateway_1m0d8gl" targetRef="Activity_1m11o8u">
      <bpmn:conditionExpression xsi:type="bpmn:tFormalExpression">=(isDecision != null and isDecision = "DONE")</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:sequenceFlow id="Flow_1me1h4k" name="BOT Unsuccessful" sourceRef="Gateway_1x2uyvd" targetRef="Activity_0ahc8wh">
      <bpmn:conditionExpression xsi:type="bpmn:tFormalExpression">=isBOTResponse != null and isBOTResponse = "UNSUCCESSFUL"</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:sequenceFlow id="Flow_0q0mi23" sourceRef="Activity_0ahc8wh" targetRef="Activity_1jxn3p2" />
    <bpmn:sequenceFlow id="Flow_1frc3u0" sourceRef="Activity_1b3t5ut" targetRef="Activity_07vkhur" />
    <bpmn:sequenceFlow id="Flow_1tbbpge" sourceRef="Activity_07vkhur" targetRef="Event_1wb5nu1" />
    <bpmn:sequenceFlow id="Flow_0b5yyjm" sourceRef="Event_1wb5nu1" targetRef="Gateway_1x2uyvd" />
    <bpmn:sequenceFlow id="Flow_0swc3cq" name="BOT Successful" sourceRef="Gateway_1x2uyvd" targetRef="Activity_1m11o8u">
      <bpmn:conditionExpression xsi:type="bpmn:tFormalExpression">=isBOTResponse != null and isBOTResponse = "SUCCESSFUL"</bpmn:conditionExpression>
    </bpmn:sequenceFlow>
    <bpmn:sequenceFlow id="Flow_1nxr4bh" sourceRef="Activity_0jo75v6" targetRef="Event_0f9xpwo" />
    <bpmn:sequenceFlow id="Flow_02nqtzg" sourceRef="Activity_1mjo9h7" targetRef="Activity_0jo75v6" />
    <bpmn:sequenceFlow id="Flow_1isiio8" sourceRef="Activity_1m11o8u" targetRef="Activity_1mjo9h7" />
    <bpmn:sequenceFlow id="Flow_143njox" sourceRef="Activity_14sj7kt" targetRef="Activity_0cwmd8n" />
    <bpmn:exclusiveGateway id="Gateway_0ujr21r">
      <bpmn:incoming>Flow_1mymxq8</bpmn:incoming>
      <bpmn:outgoing>Flow_0lmnbph</bpmn:outgoing>
      <bpmn:outgoing>Flow_1ovgttr</bpmn:outgoing>
      <bpmn:outgoing>Flow_1vvedca</bpmn:outgoing>
    </bpmn:exclusiveGateway>
    <bpmn:exclusiveGateway id="Gateway_1m0d8gl">
      <bpmn:incoming>Flow_167y00y</bpmn:incoming>
      <bpmn:incoming>Flow_0lmnbph</bpmn:incoming>
      <bpmn:outgoing>Flow_15xh55c</bpmn:outgoing>
    </bpmn:exclusiveGateway>
    <bpmn:scriptTask id="Activity_0ahc8wh" name="Update BOT Queue into UserTask">
      <bpmn:extensionElements>
        <zeebe:script expression="=destinationQueue != null and candidategroup = destinationQueue" resultVariable="destinationQueue" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_1me1h4k</bpmn:incoming>
      <bpmn:outgoing>Flow_0q0mi23</bpmn:outgoing>
    </bpmn:scriptTask>
    <bpmn:serviceTask id="Activity_07vkhur" name="Publish Message to Robotics">
      <bpmn:extensionElements>
        <zeebe:taskDefinition type="nao-process-publishRoboticTopic" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_1frc3u0</bpmn:incoming>
      <bpmn:outgoing>Flow_1tbbpge</bpmn:outgoing>
    </bpmn:serviceTask>
    <bpmn:serviceTask id="Activity_1b3t5ut" name="Update the change history about BOT Call">
      <bpmn:extensionElements>
        <zeebe:taskDefinition type="nao-process-logChangeHistoryBeforeBOTCall" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_1ovgttr</bpmn:incoming>
      <bpmn:outgoing>Flow_1frc3u0</bpmn:outgoing>
    </bpmn:serviceTask>
    <bpmn:exclusiveGateway id="Gateway_1x2uyvd">
      <bpmn:incoming>Flow_0b5yyjm</bpmn:incoming>
      <bpmn:outgoing>Flow_0swc3cq</bpmn:outgoing>
      <bpmn:outgoing>Flow_1me1h4k</bpmn:outgoing>
    </bpmn:exclusiveGateway>
    <bpmn:endEvent id="Event_0f9xpwo" name="End">
      <bpmn:incoming>Flow_1nxr4bh</bpmn:incoming>
    </bpmn:endEvent>
    <bpmn:intermediateCatchEvent id="Event_1wb5nu1" name="Wait for IGO/NIGO from BOT">
      <bpmn:incoming>Flow_1tbbpge</bpmn:incoming>
      <bpmn:outgoing>Flow_0b5yyjm</bpmn:outgoing>
      <bpmn:messageEventDefinition id="MessageEventDefinition_1qn8nbq" messageRef="Message_1tmqjmr" />
    </bpmn:intermediateCatchEvent>
    <bpmn:serviceTask id="Activity_0jo75v6" name="Log RDM API Output Data">
      <bpmn:extensionElements>
        <zeebe:taskDefinition type="nao-process-logRDMAPIOutput" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_02nqtzg</bpmn:incoming>
      <bpmn:outgoing>Flow_1nxr4bh</bpmn:outgoing>
    </bpmn:serviceTask>
    <bpmn:serviceTask id="Activity_1m11o8u" name="Log Review History">
      <bpmn:extensionElements>
        <zeebe:taskDefinition type="nao-process-logReviewHistoryAfterSecondRule" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_15xh55c</bpmn:incoming>
      <bpmn:incoming>Flow_0swc3cq</bpmn:incoming>
      <bpmn:outgoing>Flow_1isiio8</bpmn:outgoing>
    </bpmn:serviceTask>
    <bpmn:serviceTask id="Activity_14sj7kt" name="Call Account DCTM API Worker">
      <bpmn:extensionElements>
        <zeebe:taskDefinition type="nao-process-callDCTMAPIBeforeSecRule" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_1vvedca</bpmn:incoming>
      <bpmn:outgoing>Flow_143njox</bpmn:outgoing>
    </bpmn:serviceTask>
    <bpmn:callActivity id="Activity_0cwmd8n" name="Call Task Router Secondary Rule">
      <bpmn:extensionElements>
        <zeebe:calledElement processId="bopm-task-router" propagateAllChildVariables="false" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_143njox</bpmn:incoming>
      <bpmn:outgoing>Flow_167y00y</bpmn:outgoing>
    </bpmn:callActivity>
    <bpmn:serviceTask id="Activity_1mjo9h7" name="Call RDM API">
      <bpmn:extensionElements>
        <zeebe:taskDefinition type="nao-process-callRDMAPI" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_1isiio8</bpmn:incoming>
      <bpmn:outgoing>Flow_02nqtzg</bpmn:outgoing>
    </bpmn:serviceTask>
    <bpmn:sequenceFlow id="Flow_1ipzeyu" sourceRef="Activity_1jxn3p2" targetRef="Activity_1byn9g1" />
    <bpmn:sequenceFlow id="Flow_1mymxq8" sourceRef="Activity_1byn9g1" targetRef="Gateway_0ujr21r" />
    <bpmn:serviceTask id="Activity_1byn9g1" name="Update Change History">
      <bpmn:extensionElements>
        <zeebe:taskDefinition type="nao-process-logChangeHistoryAfterPrimRouter" />
      </bpmn:extensionElements>
      <bpmn:incoming>Flow_1ipzeyu</bpmn:incoming>
      <bpmn:outgoing>Flow_1mymxq8</bpmn:outgoing>
    </bpmn:serviceTask>
    <bpmn:association id="Association_1xsu9wi" associationDirection="None" sourceRef="Activity_0jo75v6" targetRef="TextAnnotation_0jblcdl" />
    <bpmn:association id="Association_0k7zi62" associationDirection="None" sourceRef="Activity_14sj7kt" targetRef="TextAnnotation_14n4h53" />
  </bpmn:process>
  <bpmn:message id="Message_063n2r5" name="Message_063n2r5" />
  <bpmn:message id="Message_1tmqjmr" name="BOTCompletion">
    <bpmn:extensionElements>
      <zeebe:subscription correlationKey="=request_id" />
    </bpmn:extensionElements>
  </bpmn:message>
  <bpmndi:BPMNDiagram id="BPMNDiagram_1">
    <bpmndi:BPMNPlane id="BPMNPlane_1" bpmnElement="Collaboration_01ohlww">
      <bpmndi:BPMNShape id="Participant_01ldumh_di" bpmnElement="Participant_01ldumh" isHorizontal="true">
        <dc:Bounds x="129" y="80" width="1751" height="1040" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Lane_0492jwa_di" bpmnElement="Lane_0492jwa" isHorizontal="true">
        <dc:Bounds x="159" y="950" width="1721" height="170" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Lane_1lio5cz_di" bpmnElement="Lane_1lio5cz" isHorizontal="true">
        <dc:Bounds x="159" y="80" width="1721" height="140" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Lane_0xx3o0a_di" bpmnElement="Lane_0xx3o0a" isHorizontal="true">
        <dc:Bounds x="159" y="220" width="1721" height="730" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_15afmdn_di" bpmnElement="Activity_0b2ramb">
        <dc:Bounds x="310" y="500" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="_BPMNShape_StartEvent_2" bpmnElement="StartEvent_1">
        <dc:Bounds x="202" y="522" width="36" height="36" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_0efoxqy_di" bpmnElement="Activity_0pq5ibg" bioc:stroke="#6b3c00" bioc:fill="#ffe0b2" color:background-color="#ffe0b2" color:border-color="#6b3c00">
        <dc:Bounds x="520" y="500" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_0d9s3yh_di" bpmnElement="Activity_1jxn3p2" bioc:stroke="#0d4372" bioc:fill="#bbdefb" color:background-color="#bbdefb" color:border-color="#0d4372">
        <dc:Bounds x="755" y="500" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_0ujr21r_di" bpmnElement="Gateway_0ujr21r" isMarkerVisible="true">
        <dc:Bounds x="1135" y="515" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_1m0d8gl_di" bpmnElement="Gateway_1m0d8gl" isMarkerVisible="true">
        <dc:Bounds x="1325" y="515" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1jcks8u_di" bpmnElement="Activity_0ahc8wh">
        <dc:Bounds x="1270" y="620" width="100" height="80" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_05fzhl8_di" bpmnElement="Activity_07vkhur" bioc:stroke="#6b3c00" bioc:fill="#ffe0b2" color:background-color="#ffe0b2" color:border-color="#6b3c00">
        <dc:Bounds x="1110" y="970" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_19hih11_di" bpmnElement="Activity_1b3t5ut">
        <dc:Bounds x="1110" y="760" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Gateway_1x2uyvd_di" bpmnElement="Gateway_1x2uyvd" isMarkerVisible="true">
        <dc:Bounds x="1575" y="635" width="50" height="50" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_0f9xpwo_di" bpmnElement="Event_0f9xpwo">
        <dc:Bounds x="1752" y="522" width="36" height="36" />
        <bpmndi:BPMNLabel>
          <dc:Bounds x="1760" y="565" width="20" height="14" />
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Event_0k23i0t_di" bpmnElement="Event_1wb5nu1" bioc:stroke="#6b3c00" bioc:fill="#ffe0b2" color:background-color="#ffe0b2" color:border-color="#6b3c00">
        <dc:Bounds x="1582" y="992" width="36" height="36" />
        <bpmndi:BPMNLabel>
          <dc:Bounds x="1562" y="1035" width="77" height="40" />
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_0rgze3e_di" bpmnElement="Activity_0jo75v6">
        <dc:Bounds x="1720" y="370" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_0zeck1t_di" bpmnElement="Activity_1m11o8u">
        <dc:Bounds x="1490" y="400" width="100" height="80" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_12kbg5y_di" bpmnElement="Activity_14sj7kt" bioc:stroke="#6b3c00" bioc:fill="#ffe0b2" color:background-color="#ffe0b2" color:border-color="#6b3c00">
        <dc:Bounds x="1110" y="402" width="100" height="80" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_19xtpn3_di" bpmnElement="Activity_0cwmd8n" bioc:stroke="#0d4372" bioc:fill="#bbdefb" color:background-color="#bbdefb" color:border-color="#0d4372">
        <dc:Bounds x="1110" y="286" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_1alssxi_di" bpmnElement="Activity_1mjo9h7" bioc:stroke="#6b3c00" bioc:fill="#ffe0b2" color:background-color="#ffe0b2" color:border-color="#6b3c00">
        <dc:Bounds x="1490" y="100" width="100" height="80" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="Activity_0et9t7o_di" bpmnElement="Activity_1byn9g1">
        <dc:Bounds x="920" y="500" width="100" height="80" />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNEdge id="Association_1xsu9wi_di" bpmnElement="Association_1xsu9wi">
        <di:waypoint x="1771" y="370" />
        <di:waypoint x="1772" y="328" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Association_0k7zi62_di" bpmnElement="Association_0k7zi62">
        <di:waypoint x="1110" y="413" />
        <di:waypoint x="940" y="312" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0mm47u4_di" bpmnElement="Flow_0mm47u4">
        <di:waypoint x="238" y="540" />
        <di:waypoint x="310" y="540" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1vfcao6_di" bpmnElement="Flow_1vfcao6">
        <di:waypoint x="410" y="540" />
        <di:waypoint x="520" y="540" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0sgm0h0_di" bpmnElement="Flow_0sgm0h0">
        <di:waypoint x="620" y="540" />
        <di:waypoint x="755" y="540" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0lmnbph_di" bpmnElement="Flow_0lmnbph">
        <di:waypoint x="1185" y="540" />
        <di:waypoint x="1325" y="540" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1ovgttr_di" bpmnElement="Flow_1ovgttr">
        <di:waypoint x="1160" y="565" />
        <di:waypoint x="1160" y="760" />
        <bpmndi:BPMNLabel>
          <dc:Bounds x="1162" y="625" width="76" height="40" />
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1vvedca_di" bpmnElement="Flow_1vvedca">
        <di:waypoint x="1160" y="515" />
        <di:waypoint x="1160" y="482" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_167y00y_di" bpmnElement="Flow_167y00y">
        <di:waypoint x="1210" y="326" />
        <di:waypoint x="1350" y="326" />
        <di:waypoint x="1350" y="515" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_15xh55c_di" bpmnElement="Flow_15xh55c">
        <di:waypoint x="1375" y="540" />
        <di:waypoint x="1520" y="540" />
        <di:waypoint x="1520" y="480" />
        <bpmndi:BPMNLabel>
          <dc:Bounds x="1408" y="522" width="80" height="27" />
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1me1h4k_di" bpmnElement="Flow_1me1h4k">
        <di:waypoint x="1575" y="660" />
        <di:waypoint x="1370" y="660" />
        <bpmndi:BPMNLabel>
          <dc:Bounds x="1448" y="666" width="66" height="27" />
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0q0mi23_di" bpmnElement="Flow_0q0mi23">
        <di:waypoint x="1270" y="660" />
        <di:waypoint x="805" y="660" />
        <di:waypoint x="805" y="580" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1frc3u0_di" bpmnElement="Flow_1frc3u0">
        <di:waypoint x="1160" y="840" />
        <di:waypoint x="1160" y="970" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1tbbpge_di" bpmnElement="Flow_1tbbpge">
        <di:waypoint x="1210" y="1010" />
        <di:waypoint x="1582" y="1010" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0b5yyjm_di" bpmnElement="Flow_0b5yyjm">
        <di:waypoint x="1600" y="992" />
        <di:waypoint x="1600" y="685" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_0swc3cq_di" bpmnElement="Flow_0swc3cq">
        <di:waypoint x="1600" y="635" />
        <di:waypoint x="1600" y="558" />
        <di:waypoint x="1570" y="558" />
        <di:waypoint x="1570" y="480" />
        <bpmndi:BPMNLabel>
          <dc:Bounds x="1545" y="519" width="80" height="14" />
        </bpmndi:BPMNLabel>
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1nxr4bh_di" bpmnElement="Flow_1nxr4bh">
        <di:waypoint x="1770" y="450" />
        <di:waypoint x="1770" y="522" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_02nqtzg_di" bpmnElement="Flow_02nqtzg">
        <di:waypoint x="1590" y="140" />
        <di:waypoint x="1770" y="140" />
        <di:waypoint x="1770" y="370" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1isiio8_di" bpmnElement="Flow_1isiio8">
        <di:waypoint x="1540" y="400" />
        <di:waypoint x="1540" y="180" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_143njox_di" bpmnElement="Flow_143njox">
        <di:waypoint x="1160" y="402" />
        <di:waypoint x="1160" y="366" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1ipzeyu_di" bpmnElement="Flow_1ipzeyu">
        <di:waypoint x="855" y="540" />
        <di:waypoint x="920" y="540" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Flow_1mymxq8_di" bpmnElement="Flow_1mymxq8">
        <di:waypoint x="1020" y="540" />
        <di:waypoint x="1135" y="540" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Association_091rpvg_di" bpmnElement="Association_091rpvg">
        <di:waypoint x="584" y="500" />
        <di:waypoint x="601" y="451" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Association_0syytw4_di" bpmnElement="Association_0syytw4">
        <di:waypoint x="815" y="500" />
        <di:waypoint x="827" y="451" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Association_1xwtn2y_di" bpmnElement="Association_1xwtn2y">
        <di:waypoint x="1210" y="795" />
        <di:waypoint x="1350" y="778" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Association_06u1xqp_di" bpmnElement="Association_06u1xqp">
        <di:waypoint x="1192" y="970" />
        <di:waypoint x="1224" y="930" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Association_1dh6g8i_di" bpmnElement="Association_1dh6g8i">
        <di:waypoint x="1192" y="286" />
        <di:waypoint x="1220" y="250" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Association_017keau_di" bpmnElement="Association_017keau">
        <di:waypoint x="1610" y="995" />
        <di:waypoint x="1671" y="910" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Association_1qfcwh0_di" bpmnElement="Association_1qfcwh0">
        <di:waypoint x="1590" y="117" />
        <di:waypoint x="1650" y="90" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Association_13lumkf_di" bpmnElement="Association_13lumkf">
        <di:waypoint x="1160" y="499" />
        <di:waypoint x="1230" y="491" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Association_03ix82b_di" bpmnElement="Association_03ix82b">
        <di:waypoint x="1255" y="540" />
        <di:waypoint x="1274" y="560" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNEdge id="Association_1ism3za_di" bpmnElement="Association_1ism3za">
        <di:waypoint x="1333" y="326" />
        <di:waypoint x="1390" y="339" />
      </bpmndi:BPMNEdge>
      <bpmndi:BPMNShape id="TextAnnotation_0n814vb_di" bpmnElement="TextAnnotation_0n814vb">
        <dc:Bounds x="560" y="410" width="100" height="41" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="TextAnnotation_1rsmd3f_di" bpmnElement="TextAnnotation_1rsmd3f">
        <dc:Bounds x="780" y="381" width="170" height="70" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="TextAnnotation_0jblcdl_di" bpmnElement="TextAnnotation_0jblcdl">
        <dc:Bounds x="1720" y="301" width="251" height="27" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="TextAnnotation_14n4h53_di" bpmnElement="TextAnnotation_14n4h53">
        <dc:Bounds x="730" y="268" width="210" height="60" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="TextAnnotation_0n1ta3o_di" bpmnElement="TextAnnotation_0n1ta3o">
        <dc:Bounds x="1350" y="758" width="100" height="84" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="TextAnnotation_1po6hnl_di" bpmnElement="TextAnnotation_1po6hnl">
        <dc:Bounds x="1190" y="894" width="314" height="36" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="TextAnnotation_01dztd0_di" bpmnElement="TextAnnotation_01dztd0">
        <dc:Bounds x="1190" y="200" width="130" height="50" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="TextAnnotation_0vocrsv_di" bpmnElement="TextAnnotation_0vocrsv">
        <dc:Bounds x="1660" y="840" width="220" height="70" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="TextAnnotation_1n58fkh_di" bpmnElement="TextAnnotation_1n58fkh">
        <dc:Bounds x="1650" y="50" width="170" height="55" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="TextAnnotation_1dpnhxg_di" bpmnElement="TextAnnotation_1dpnhxg">
        <dc:Bounds x="1230" y="470" width="100" height="30" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="TextAnnotation_0y0fy0b_di" bpmnElement="TextAnnotation_0y0fy0b">
        <dc:Bounds x="1240" y="560" width="100" height="30" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
      <bpmndi:BPMNShape id="TextAnnotation_04uaz4w_di" bpmnElement="TextAnnotation_04uaz4w">
        <dc:Bounds x="1390" y="316" width="134" height="69" />
        <bpmndi:BPMNLabel />
      </bpmndi:BPMNShape>
    </bpmndi:BPMNPlane>
  </bpmndi:BPMNDiagram>
</bpmn:definitions>



package com.bopm.workflow.worker;

import java.util.Map;

import org.json.JSONObject;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import com.bopm.workflow.service.DatabaseService;

import io.camunda.zeebe.client.api.response.ActivatedJob;
import io.camunda.zeebe.client.api.worker.JobClient;
import io.camunda.zeebe.spring.client.annotation.JobWorker;

@Component
public class NaoWorker {

	@Autowired
	DatabaseService databaseService;
	
    private final static Logger LOG = LoggerFactory.getLogger(NaoWorker.class);
	
	
	@JobWorker(type = "LogNAOData", autoComplete = false) 
	public void insertData(final ActivatedJob job, final JobClient client) {

		JSONObject piDataJson = new JSONObject(job.getVariables()); 

		boolean logTransactionStatus = false;
		LOG.info("InsertData: START with input parameter = " + job.getProcessInstanceKey() + ",data ="
				+ piDataJson);
		try {
			piDataJson.put("logTransactionStatus", logTransactionStatus);
			databaseService.insertProcessData(String.valueOf(job.getProcessInstanceKey()),
					piDataJson.getString("processName"), piDataJson);
			client.newCompleteCommand(job.getKey()).variables(piDataJson.toString()).send().join();
			LOG.info("Insert in db complete...");
		} catch (Exception ex) {
			LOG.error("Error in LogNAOData worker: insertData, error: " + ex.getMessage());
			try {

				client.newFailCommand(job).retries(job.getRetries() - 1).errorMessage(ex.toString()).send().wait(1000);
			} catch (InterruptedException e) {
		
				LOG.info("Error in LogNAOData worker:insertData  :" + e.getMessage());
			}
		}
	}
	
}




package com.bopm.workflow.service.impl;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.text.SimpleDateFormat;
import java.time.LocalDateTime;
import java.util.Date;

import javax.annotation.PostConstruct;

import org.json.JSONObject;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.bopm.workflow.config.GlobalValueConfig;
import com.bopm.workflow.service.DatabaseService;
import com.bopm.workflow.util.BOPMStatusEnum;
import com.bopm.workflow.util.GeneralConstants;
import com.bopm.workflow.worker.NaoWorker;
import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;

@Service
public class DatabaseServiceImpl implements DatabaseService {

	@Autowired
	GlobalValueConfig globalConfig;

    private final static Logger LOG = LoggerFactory.getLogger(NaoWorker.class);

    HikariConfig config = new HikariConfig(); // Configuration for Hikari connection pool
    HikariDataSource ds; // Hikari DataSource

    // Method to check database connection after service is initialized
    @PostConstruct
    public void checkDatabaseConnection () {
        try {
        	databaseConnectionPool (); // Initialize the database connection pool
        } catch (SQLException ex) {
            LOG.error("Error while initializing database connection pool", ex); 

        }
    }
    // This method sets up the connection pool
    public void databaseConnectionPool () throws SQLException {
        String databaseName = "bopm";
        String dbUrl = globalConfig.dbhost;
        String url = "jdbc:postgresql://" + dbUrl + databaseName;
        String user = globalConfig.dbUsername;
        String password = globalConfig.dbPassword;

        config.setJdbcUrl(url);
        config.setUsername(user);
        config.setPassword(password);
        ds = new HikariDataSource(config); // Connection pool is set up here
    }

    // This method gets a connection from the pool
    public Connection getConnection() throws SQLException {
        return ds.getConnection(); // Connection is obtained from the pool here
    }

    public boolean insertProcessData(String processInstanceKey, String processName, JSONObject processDetails)
            throws Exception {

        String INSERT_SQL = "call " + GeneralConstants.PROCEDURE_TO_INSERT_DATA;

        LOG.info("Method name :InsertProcessData START with input parameter" + processInstanceKey);

        // Try-with-resources is used here to automatically close the connection and preparedStatement
		try (Connection connection = getConnection();
				PreparedStatement preparedStatement = connection.prepareStatement(INSERT_SQL)) {

			SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss");
			SimpleDateFormat output = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");// "yyyy-MM-dd HH:mm:ss.SSSSSS")
			Date d = sdf.parse(processDetails.getString("creation_date"));
			String formattedTime = output.format(d);
			preparedStatement.setObject(1, processInstanceKey, java.sql.Types.BIGINT); // ProcessInstanceKEy
			preparedStatement.setObject(2, 1, java.sql.Types.SMALLINT); // ProcessId
			preparedStatement.setObject(3, LocalDateTime.now(), java.sql.Types.TIMESTAMP); // StartDate
			preparedStatement.setObject(4, null);// NOSONAR // EndDate
			preparedStatement.setObject(5, formattedTime, java.sql.Types.TIMESTAMP);// RequestDate //creation_date
			preparedStatement.setObject(6, processDetails.getString("document_date"));// NOSONAR // DocumentDate
			preparedStatement.setString(7, processDetails.getString("image_rep_id"));// Rep_id
			preparedStatement.setString(8, GeneralConstants.STATUS_ACTIVE);// ProcessIntsanceStatus
			preparedStatement.setShort(9, BOPMStatusEnum.NEW.getId());// RequestStatus

			preparedStatement.setString(10, processDetails.getString("source_id"));// source_id -> RequestId
			preparedStatement.setString(11, processDetails.getString("image_ssn"));// image_ssn -> SSN
			preparedStatement.setString(12, "");// NOSONAR// Assignee
			preparedStatement.setObject(13, processDetails, java.sql.Types.OTHER);// ProcessInstanceJSON
			preparedStatement.setObject(14, processDetails.getString("firm_id"));// NOSONAR // firmid
			preparedStatement.setString(15, processDetails.getString("sub_firm"));// NOSONAR // subfirmid
			preparedStatement.setString(16, null);// CreatedBy
			preparedStatement.setString(17, null);// UpdatedBy
			preparedStatement.setObject(18, LocalDateTime.now(), java.sql.Types.TIMESTAMP);// UpdatedDate
			preparedStatement.setObject(19, processDetails.getString("account_number"));// accountnumber

			 preparedStatement.executeUpdate();
	            return true;
	        } catch (SQLException ex) {
	            LOG.error(GeneralConstants.DATABASE_ERROR
	                    + " DatabaseServiceImpl --> InsertProcessData : Error, Error Message: " + ex.toString()
	                    + ", processInstanceKey:" + processInstanceKey);
	            throw new Exception(ex.getMessage());
	        } // Connection and preparedStatement are automatically closed here
	    }
	}

