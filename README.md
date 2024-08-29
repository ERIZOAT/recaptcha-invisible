<img width="960" alt="reCaptcha v2 invisible solver" src="https://github.com/user-attachments/assets/7bcddc7e-1079-47b4-b8b4-bc60df3be349">

# How to Identify and Solve reCaptcha v2 Invisible with CapSolver

This repository demonstrates how to effectively identify and solve reCaptcha v2 invisible using [CapSolver](https://www.capsolver.com/?utm_source=github&utm_medium=repo&utm_campaign=recaptchainvisible)’s services.

## Identifying the Correct reCaptcha Version

Before solving reCaptcha v2 invisible, it is crucial to verify that the captcha is indeed reCaptcha v2 invisible and not another version.

### Identifying the reCaptcha Version

You can use CapSolver's browser extension to identify the captcha version and its parameters with 100% accuracy. The extension not only determines the captcha version but also retrieves all relevant parameters required for solving it.

![Extension Example](https://assets.capsolver.com/prod/images/post/2023-11-06/ddf61de6-a736-421a-b186-482b3940afc7.png)

For step-by-step instructions on using this extension, refer to the [Instruction Manual for reCaptcha Identification Extension](https://www.capsolver.com/blog/Extension/identify-any-captcha-and-parameters).

### Retrieving Capsolver JSON

Once you've confirmed the presence of reCaptcha v2 invisible, the CapSolver extension will provide a JSON structure similar to this:

```json
{
    "type": "ReCaptchaV2TaskProxyLess",
    "websiteURL": "https://example.com",
    "websiteKey": "6LcR_okUAAAAAPYrPe-HK_0RULO1aZM15ENyM-Mf",
    "anchor": "value",
    "reload": "value",
    "isInvisible": true
}
```

### Using the JSON with CapSolver API

With the JSON in hand, you're ready to proceed with solving the reCaptcha.

## Solving reCaptcha v2 Invisible

To solve reCaptcha v2 invisible, follow these steps:

### Step 1: Create a Task

You can create a task by sending a POST request to the CapSolver API. Below is an example request:

```json
POST https://api.capsolver.com/createTask
Host: api.capsolver.com
Content-Type: application/json
{
    "clientKey": "YOUR_API_KEY",
    "task": {
        "type": "ReCaptchaV2TaskProxyLess",
        "websiteURL": "https://example.com",
        "websiteKey": "6LcR_okUAAAAAPYrPe-HK_0RULO1aZM15ENyM-Mf",
        "anchor": "value",
        "reload": "value",
        "isInvisible": true
    }
}
```

You should first try the `ReCaptchaV2TaskProxyLess` type to see if it generates a valid token. If it fails, switch to the `ReCaptchaV2Task` type, which allows you to use your own proxy.

### Step 2: Get the Task Result

Once you've created the task, retrieve the result with the following request:

```json
POST https://api.capsolver.com/getTaskResult
Host: api.capsolver.com
Content-Type: application/json
{
    "clientKey": "YOUR_API_KEY",
    "taskId": "37223a89-06ed-442c-a0b8-22067b79c5b4" // Replace with the taskId from createTask response
}
```

### Example Response

You will receive a response similar to this:

```json
{
    "errorId": 0,
    "status": "ready",
    "solution": {
        "gRecaptchaResponse": "03AGdBq24o3_oGR_...6M2BOmV"
    },
    "cost": 0.0005,
    "ip": "1.2.3.4",
    "createTime": 1648060911,
    "endTime": 1648060921,
    "solveCount": 1,
    "workerId": "123456"
}
```

If the token does not work, contact [CapSolver Support](https://www.capsolver.com/?utm_source=github&utm_medium=repo&utm_campaign=recaptchainvisible) for assistance.

## References

- [CapSolver Official Website](https://www.capsolver.com/?utm_source=github&utm_medium=repo&utm_campaign=recaptchainvisible)
- [CapSolver Documentation](https://docs.capsolver.com/en/guide/getting-started/?utm_source=github&utm_medium=repo&utm_campaign=recaptchainvisible)

