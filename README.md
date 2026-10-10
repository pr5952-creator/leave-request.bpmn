# Exercise 6 — Start a Camunda 8 Process Using an API Call

## BPMN model
Open `bpmn/leave-request.bpmn` in Camunda Modeler.

- Process ID: `leave-request`
- Start event: `Leave requested`
- User task: `Approve Leave`
- End event: `Leave processed`

## Steps
1. Open `bpmn/leave-request.bpmn` in Camunda Modeler.
2. Confirm the process ID is `leave-request`.
3. Deploy the process to your Camunda 8 cluster/environment using the deployment option available in your setup.
4. In Postman, create a POST request to `http://localhost:8080/v2/process-instances`.
5. Add header `Content-Type: application/json`.
6. Choose Body → raw → JSON and send:
```json
{
  "processDefinitionId": "leave-request",
  "variables": {
    "employeeName": "Ravi",
    "days": 3
  }
}
```
7. Note the returned `processInstanceKey`.
8. In Operate, find the instance. It should be waiting at `Approve Leave`, with both variables visible.

## Viva quick answers
1. `processDefinitionId` identifies the deployed process model; `processInstanceKey` identifies one specific execution of that model.
2. If the process ID is misspelled or the process is not deployed, the API request should fail because the process definition cannot be found.
3. Starting it three times should create three instances, each with its own process instance key, visible in Operate.

## Note
This assumes your local Camunda 8 Run API is available at `http://localhost:8080`. If your instructor uses a different setup or port, use the endpoint configured for your class. The BPMN model is included; deployment and API execution must still be performed in your environment.
