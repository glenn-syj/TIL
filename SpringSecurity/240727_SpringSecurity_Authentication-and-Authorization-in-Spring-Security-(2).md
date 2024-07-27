# Authentication and Authorization in Spring Security (2)

**Disclaimer**

- Last modified(yy/mm/dd): 24/07/27
- Written By: [@glenn-syj](https://github.com/glenn-syj)

## Explanation

### Start Point

In the previous article, the difference between authenticaton and authorization was introudced. Both were related to access for resources. The former is the verification of the user who tries to access, and the latter is the filtering the access based on the level of the role or a certain kind of attribute. Spring Security consists of various and useful features for authentication. Then, how about authorization?

This article will simply explore the way the spring security helps use features for authorization.

### Tackling Curiosity

**Spring Security Authorziation**

1. Authentication

In authorization of the Spring Security, the authentication process should be validated priorly. Let's assume that authentication was successfully done.

2. SecurityContextHolder

Then, the `SecurityContextHolder` holds and manages the `SecurityContext` with `Authentication` of the current autheticated user. Here the `Authentication` holds the `GrantedAuthority` implemented through `SimpleGrantedAuthority`. When a user tries to access a certain resource, Spring Security checks whether the user has a valid authority for access.

3. Security Filter Chain

Here the `FilterSecurityInterceptor` in the security filter chain intercepts the request and fetches the metadata for the resource from `SecurityMetadataSource`.

4. AuthorizationManager

After fetching the metadata, the `AuthorizationManager` allows or denies the access based on the `Authentication` and the policy of the resource. The`check` method proceeds the authorization decision. Applications that previously used `AccessDecisionManager` or `AccessDecisionVoter`are encouraged to replace them with `AuthorizationManager`.

Furthermore, Spring Security supports a delgating `AuthorizationManager` for individual `AuthorizationManager`s like `AuthorityAuthorizationManager` and `AuthenticatedAuthorizationManager`.

5. AccessDecisionManager and AccessDecisionVoter

`AuthorizationManager` may invoke `AccessDecisionManager` or `AccessDecisionVoter`. `AccessDecisionManager` has a `decide()` method which throws `AccessDeniedException` when access is denied. The `support(ConfigAttribute)` method would be called by a security interceptor to check if the manager supports the passed `ConfigAttribute`. The `support(Class)`, the class of the passed `SecureObject`.

`AccessDecisionVoter` is based on the voting. The interface has three methods `vote(Authentication, Object, Collection<ConfigAttribute>)`, `supports(ConfigAttribute)`, `supports(Class)`. The `vote` implementation returns an `int` value that represents `ACCESS_ABSTAIN` (no opinion), `ACCESS_DENIED` (denied), and `ACCESS_GRANTED` (granted). The specific vote descriptions will be explored later.

**Hierarchial Roles**

In the world of authorization, there would commonly be cases where some roles include other roles. For example, The `ROLE_ADMIN` role might be able to do every behaviors what `ROLE_USER` can do.

The role-hierarchy supported for filter-based authorization, method-based authorization, and pre-post annotations helps configuring implications among roles.

Below is an example of using hierarchial roles in Spring Security. The code is from the spring docs, but the comment in the `roleHierarchy()` is written by myself.

```java
// https://docs.spring.io/spring-security/reference/servlet/authorization/architecture.html#authz-legacy-note

@Bean
static RoleHierarchy roleHierarchy() {
    // ROLE_ADMIN => ROLE_STAFF => ROLE_USER => ROLE_GUEST
    return RoleHierarchyImpl.withDefaultRolePrefix()
        .role("ADMIN").implies("STAFF")
        .role("STAFF").implies("USER")
        .role("USER").implies("GUEST")
        .build();
}

// and, if using pre-post method security also add
@Bean
static MethodSecurityExpressionHandler methodSecurityExpressionHandler(RoleHierarchy roleHierarchy) {
	DefaultMethodSecurityExpressionHandler expressionHandler = new DefaultMethodSecurityExpressionHandler();
	expressionHandler.setRoleHierarchy(roleHierarchy);
	return expressionHandler;
}
```

### References

https://docs.spring.io/spring-security/reference/servlet/authorization/architecture.html
