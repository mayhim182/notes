Webhooks allow systems to send real-time notifications triggered by specific events. Unlike traditional APIs, which rely on polling, webhooks push data immediately when an event occurs, making them highly efficient and real-time.

![[Pasted image 20250830221908.png]]

## Functional Requirements
### Core Requirements

1. **Accept API Calls to Receive Event Notifications**: Accept API calls to receive event notifications (e.g., payment processed or order shipped), execute corresponding operations, and persist original event data and operation results for tracking, auditing, and debugging.
    
2. **High Availability and Resilience**: The service must ensure events are processed even if system components fail, maintaining reliability for critical data.

### Scale Requirements

- Event Volume: The system should handle 1 million events per day.
- Traffic Spikes: During peak hours, incoming requests may increase by 5 times.
- Latency Requirement: End-to-end latency (from event arrival to processing completion) should be under 200 milliseconds.
- Data Retention: The system should store all events for 30 days. Assume each event is 5KB.

## Non-Functional Requirements

- High availability: The system should be highly available and resilient to failures.
- Low latency: As mentioned in the scale requirement, end-to-end latency should be under 200 milliseconds.
- At-least-once processing: Each event should be processed at least once if the system accepts it.
  
## API Endpoints

#### POST /webhook

Receive webhooks from external systems, returns 200 OK if the event is accepted.

**Response Body:**

`{   "status": "success" }`

![[Pasted image 20250831021722.png]]

![[Pasted image 20250831021748.png]]
![[Pasted image 20250831021809.png]]