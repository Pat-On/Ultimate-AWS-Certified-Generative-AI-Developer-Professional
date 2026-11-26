# 158. Amazon API Gateway Hands On

- **Type:** Practice lab

## Create the API

- API types offered: **HTTP**, **WebSocket** and **REST** (public or private). The lab uses **REST**.
- A REST API can be new, **imported from OpenAPI**, cloned or built from the example. Here: new, named `MyFirstAPI`, endpoint type **Regional**.

## First method: `GET /`

1. Create a **GET** method. Integration types: **Lambda function**, **HTTP**, **Mock**, **AWS service**, **VPC link**.
2. Create a Python Lambda (`api-gateway-route-gets`) returning status **200**, a `Content-Type: application/json` header and a JSON body "Hello from Lambda". Deploy it and run a test event.
3. Paste the function **ARN** into the method and enable **Lambda proxy integration**, so the full request reaches Lambda and its response is interpreted by API Gateway.

## Things to notice

- **Timeout:** API Gateway waits **29 seconds** by default, even though Lambda can run for up to 15 minutes. You can set it lower.
- **Permissions:** creating the method adds a **resource-based policy** to the function that lets this API invoke it (Configuration → Permissions).
- **Testing:** the console test shows status, body, headers and the **execution log**, which helps debugging.
- **Event:** printing the event to **CloudWatch Logs** shows what the function receives: resource, path, HTTP method, headers, query string parameters and more.

## Second route and deployment

1. Create the resource **`/houses`** with its own GET method, proxying to a **second Lambda function**.
2. **Deploy API** to a new **stage** called `dev`. This gives an **invoke URL**.
3. In a browser, `/dev` and `/dev/houses` answer from the two functions. An unknown path returns **"Missing Authentication Token"**.

**Beyond the lecture:** for Regional and private REST APIs, AWS now allows raising the 29-second limit through a quota increase.

## Exam takeaways

1. **Lambda proxy integration** passes the whole request through; the function builds the status, headers and body.
2. Remember the **29-second** integration timeout.
3. Changes are reachable only after you **deploy to a stage**.
