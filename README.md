
# Getting Started with Swagger Petstore

## Introduction

This is a sample server Petstore server.  You can find out more about Swagger at [http://swagger.io](http://swagger.io) or on [irc.freenode.net, #swagger](http://swagger.io/irc/).  For this sample, you can use the api key `special-key` to test the authorization filters.

Find out more about Swagger: [http://swagger.io](http://swagger.io)

## Install the Package

Run the following command to install the package and automatically add the dependency to your composer.json file:

```bash
composer require "zahra/rose-test-sdk:0.0.9"
```

Or add it to the composer.json file manually as given below:

```json
"require": {
    "zahra/rose-test-sdk": "0.0.9"
}
```

You can also view the package at:
https://packagist.org/packages/zahra/rose-test-sdk#0.0.9

## Test the SDK

Unit tests in this SDK can be run using PHPUnit.

1. First install the dependencies using composer including the `require-dev` dependencies.
2. Run `vendor\bin\phpunit --verbose` from commandline to execute tests. If you have installed PHPUnit globally, run tests using `phpunit --verbose` instead.

You can change the PHPUnit test configuration in the `phpunit.xml` file.

## Initialize the API Client

**_Note:_** Documentation for the client can be found [here.](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/client.md)

The following parameters are configurable for the API Client:

| Parameter | Type | Description |
|  --- | --- | --- |
| testHeader | `string` | This is a test header<br>*Default*: `'TestHeaderDefaultValue'` |
| environment | `Environment` | The API environment. <br> **Default: `Environment.PRODUCTION`** |
| timeout | `int` | Timeout for API calls in seconds.<br>*Default*: `0` |
| enableRetries | `bool` | Whether to enable retries and backoff feature.<br>*Default*: `false` |
| numberOfRetries | `int` | The number of retries to make.<br>*Default*: `0` |
| retryInterval | `float` | The retry time interval between the endpoint calls.<br>*Default*: `1` |
| backOffFactor | `float` | Exponential backoff factor to increase interval between retries.<br>*Default*: `2` |
| maximumRetryWaitTime | `int` | The maximum wait time in seconds for overall retrying requests.<br>*Default*: `0` |
| retryOnTimeout | `bool` | Whether to retry on request timeout.<br>*Default*: `true` |
| httpStatusCodesToRetry | `array` | Http status codes to retry against.<br>*Default*: `408, 413, 429, 500, 502, 503, 504, 521, 522, 524` |
| httpMethodsToRetry | `array` | Http methods to retry against.<br>*Default*: `'GET', 'PUT'` |
| proxyConfiguration | [`ProxyConfigurationBuilder`](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/proxy-configuration-builder.md) | Represents the proxy configurations for API calls |
| apiKeyCredentials | [`ApiKeyCredentials`](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/auth/custom-header-signature.md) | The Credentials Setter for Custom Header Signature |
| httpBasicCredentials | [`HttpBasicCredentials`](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/auth/basic-authentication.md) | The Credentials Setter for Basic Authentication |
| petstoreAuthCredentials | [`PetstoreAuthCredentials`](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/auth/oauth-2-implicit-grant.md) | The Credentials Setter for OAuth 2 Implicit Grant |

The API client can be initialized as follows:

```php
use SwaggerPetstoreLib\Environment;
use SwaggerPetstoreLib\Authentication\ApiKeyCredentialsBuilder;
use SwaggerPetstoreLib\Authentication\HttpBasicCredentialsBuilder;
use SwaggerPetstoreLib\Authentication\PetstoreAuthCredentialsBuilder;
use SwaggerPetstoreLib\Models\OAuthScopePetstoreAuthEnum;
use SwaggerPetstoreLib\SwaggerPetstoreClientBuilder;

$client = SwaggerPetstoreClientBuilder::init()
    ->apiKeyCredentials(
        ApiKeyCredentialsBuilder::init(
            'api_key'
        )
    )
    ->httpBasicCredentials(
        HttpBasicCredentialsBuilder::init(
            'username',
            'passwprd'
        )
    )
    ->petstoreAuthCredentials(
        PetstoreAuthCredentialsBuilder::init(
            'OAuthClientId',
            'OAuthRedirectUri'
        )
            ->oAuthScopes(
                [
                    OAuthScopePetstoreAuthEnum::READPETS,
                    OAuthScopePetstoreAuthEnum::WRITEPETS
                ]
            )
    )
    ->testHeader('TestHeaderDefaultValue')
    ->environment(Environment::PRODUCTION)
    ->build();
```

## Environments

The SDK can be configured to use a different environment for making API calls. Available environments are:

### Fields

| Name | Description |
|  --- | --- |
| production | **Default** |
| environment2 | - |
| environment3 | - |

## Authorization

This API uses the following authentication schemes.

* [`api_key (Custom Header Signature)`](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/auth/custom-header-signature.md)
* [`httpBasic (Basic Authentication)`](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/auth/basic-authentication.md)
* [`petstore_auth (OAuth 2 Implicit Grant)`](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/auth/oauth-2-implicit-grant.md)

## List of APIs

* [Pet](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/controllers/pet.md)
* [Store](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/controllers/store.md)
* [User](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/controllers/user.md)

## SDK Infrastructure

### Configuration

* [ProxyConfigurationBuilder](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/proxy-configuration-builder.md)

### HTTP

* [HttpRequest](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/http-request.md)
* [HttpResponse](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/http-response.md)

### Utilities

* [FileWrapper](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/file-wrapper.md)
* [ApiException](https://www.github.com/ZahraN444/rose-test-php-sdk/tree/0.0.9/doc/api-exception.md)

