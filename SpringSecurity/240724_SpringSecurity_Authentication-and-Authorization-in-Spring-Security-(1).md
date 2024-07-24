# Authentication and Authorization in Spring Security (1)

**Disclaimer**

- Last modified(yy/mm/dd): 24/07/24
- Written By: [@glenn-syj](https://github.com/glenn-syj)

## Explanation

### Start Point

In the current project, I had been getting together with a new team due to the previous team being undermanned. The part which I am developing and refactoring is now mainly the user management. I had completed a project which uses session login without Spring Security. Before developing my own codes, apprehending and refactoring the current codes (which were not tested yet) should be preceeded.

This article features the Spring Security with the basic security concepts, especially authentication and authorization.

### Tackling Curiosity

**Authentication and Authorization**

The basic concept that authentication and authorization share is the access to a resource. However, they could easily be found different when considering the process.

Authentication is the process of identifying the user. The user credentials should be validated through passwords or answers. This step is usually done before authorization.

Authorization is the process of verifying the level of the access. It means that the access to some resource is permitted, while other resources rejected. Therefore, authorization is related to policies and rules describing the roles and responsibilites.

**Spring Security with Authn and Authz**

Spring Security serves various features related to authn(authentication), authz(authorization), and further security concerns. In this section, the simple example of authn and authz would be featured.

1. Authentication

Authn is the process of verifying who the user is. Usually, the login system becomes the authentication system. There are various authn mechanisms like Form-Login, HTTP Basic, JWT, OAuth2. Instead of describing the JWT authentication logic, I'll start with the common process with the filter login.

The main Spring Security components in the authn process are hard to choose, as the whole process consists of the powerful and important components. Please know that the description below is not based on the whole process and simplified (no filter chain logics or custom methods would be introduced here, sorry).

(1) Request from client

The client sends the login request with username and password. Here, the username does not have to always be a real user name or a nickanme. Username here means that the attribute which identifies the user.

(2) AuthenticationFilter

The request from client goes through the filter chain. The filters here are the Spring MVC filter before entering servlets. The `AuthenticatinoFilter` interface with subclass like `UsernamePasswordAuthenticationFilter` intercepts the request and delivers it to the `AuthenticationManager` in a token.

(3) AuthenticationManager

The filter before delegates the authentication to `AuthenticationManager`. It has `authenticate()` method which receives a `Authentication` type token. It would be good to know that `Authentication` interface subclass play a different role before/after the authentication. Here, before authenticated its main role is packing the username and the password.

(4) AuthenticationProvider

`AuthenticationProvider` can have multiple `AuthenticationProvider`s. Each provider proceeds a specific authentication mechanism. The proper one is chosen and proceeds the authentication.

(5) UserDetailService

`UserDetailService` returns `UserDetails` instance which loads the user detail from the respository related to the user. Its `loadUserByUsername(String username)` loads the details.

(6) Validation and Result

The user detail in the request is validated to the loaded user detail. After the successful validation, the login filter or the controller returns the response.

If authentication is successful, the `SecurityContextHolder` saves the authentication information. (`SecurityContext` would be explored later.)

When authentication is failed, the exception is thrown and the process after the failure is proceeded.

### References

https://auth0.com/docs/get-started/identity-fundamentals/authentication-and-authorization

https://medium.com/@rasheed99/introduction-on-spring-security-architecture-eb5d7de75a4f