# Ruby Tutorial

> This tutorial will help you get started with Finch API with Ruby..

## Introduction

Finch is an API that allows mobile and web applications to retrieve data and make changes to payroll/HRIS systems across providers (think "income/employment verification" or "pulling pay statements"). This tutorial will help you get up and running with the Finch API using Node along with a front-end.

## 1. Obtain an access token

With an authorization `code` you can use the Ruby client to get an `access_token`. The Ruby application must exchange the `code` for an `access_token` to make a request. After receiving the `access_token`, the user can be redirected to the `/identity` route which we will implement in the next step.

```
auth_params = {
  user: client_id,
  pass: client_secret
}

response = @client.auth.get(@code, auth_params)

access_token = response[:auth_token]
```

## 2. Get identity information

Once the application has the `access_token`, it can send requests to a payroll account using Finch's API.

```
auth = {
  bearer: access_token
}

identity_response = @client.identity(auth)

return { status: 200, identity_response.data }
```
