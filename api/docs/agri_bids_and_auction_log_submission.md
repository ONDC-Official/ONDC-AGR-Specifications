## Log submission Scenarios for bids and auction & Igm

#### Instructions

- Create a fork of the [verification-logs](https://github.com/ONDC-Official/verification-logs) repository.
- Create a folder with the name of your entity under your domain folder "AGR11" for credit.
- Commit your logs in the folder (logs should include request & response payloads for all enabled APIs as per the scenarios below).
- Create PR and label it with your domain name.
- Once submitted, please refer to the comments on logs submitted and update the PR based on the comments provided.
- Once the reviews are done, the PR will be merged and the logs shall be considered as approved on pr merge
- Both IGM and transactional logs need to be submitted in a single PR
- For IGM logs, create a folder with name igm under your entity named folder.

### File Naming conventions:

1. **Single Endpoint Naming**:

   - For a single API endpoint, the file name should precisely match the name of the endpoint. For example:
     - `search: search.json` (for the "search" endpoint)
     - `on_search: on_search.json` (for the "on_search" endpoint)
2. **Multiple Calls for Same Endpoint**:

   - When there are multiple API calls for the same endpoint, the naming convention should reflect the sequence of calls using numeric suffixes:
     - `select 1: select_1.json` (for the first call of the "select" endpoint)
     - `select 2: select_2.json` (for the second call of the "select" endpoint)
     - `init 1: init_1.json` (for the first call of the "init" endpoint)
     - `init 2: init_2.json` (for the second call of the "init" endpoint)

These naming conventions ensure clear identification and organization of files based on the corresponding API endpoints and their respective calls.

### Scenarios

- **Flow 1**

  Verify that buyers can place bids openly and see competing bids in real-time.
    - **Search**    (Trigger the search for catalog payload)
    - **On Search**    (Seller will send the catalog and buyer will cache/store it for listing)
    - **Select**    (Select the item for bids)
    - **On Select**   (Verify the item and eligibility)
    - **Init**  (If Earnest Money deposit)
    - **On Init**   (Show the Quote and Payment for Earnest Money deposit)
    - **On Status**   (Send the payment status for Earnest Money deposit)
    - **Init**  (This is for bid placement initialisation)
    - **On Init**   (This is for bid placement initialisation)
    - **Confirm**   (Buyer will confirm the order)
    - **On Confirm**  (If everything is valid then seller will accept the bid and confirm)
    - **Status**  (Buyer can check the bids status)
    - **On Status**   (Seller will confirm the status)
    - **Update**  (If buyer wants to update the bids price)
    - **On Update**   (Seller will confirm the update and send the updated quotes and payment)
    - **On Update**   (Seller will send this to the user who won the bids with awarded status)
    - **On Update**   (to rest of the user seller send the on update with not awarded status)

   
   
  ##### *Note: For rest flow see the flow UI and test case docs*




### Test Cases and Log Verification

- To submit the logs, please follow the provided link to review the test cases and the defined mandatory flow [Check here](https://docs.google.com/document/d/1O3w6UwTF3IFK-GLahtndZ7p5VgVEKb63nwNFzEIzb9E/edit?tab=t.0)

- For Igm logs, use POST api exposed at [https://log-validation.ondc.org/api/validate/igm](https://log-validation.ondc.org/api/validate/igm)

The body structure for igm logs:

```json
{
  "domain": "",
  "version": "1.0.0",
  "payload": {
    "ret_issue": {},
    "ret_issue_close": {},
    "ret_on_issue": {},
    "ret_issue_status": {},
    "ret_on_issue_status": {},
    "ret_on_issue_status_unsolicited": {}
  }
}
```

The api call sequence inside the payload object might differ based on different flows

*Note: Log verification will follow a FIFO model with a TAT of 4 days*