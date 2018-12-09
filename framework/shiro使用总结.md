---
layout: default
---

>

### 1. 动态加载拦截规则

```java
import org.apache.shiro.spring.web.ShiroFilterFactoryBean;

@Autowired
private ShiroFilterFactoryBean shiroFilterFactoryBean;

@PostConstruct
public void initPerms() {
  Map<String, String> map = new HashMap<>();
  map.put("/userManage/add","authc,roles[ADMIN]");
  shiroFilterFactoryBean.setFilterChainDefinitionMap(map);
}
```

## 2. 根据sessionId获取session

```java
String sessionId = "abc";
Session session = SecurityUtils.getSecurityManager().getSession(new DefaultSessionKey(sessionId));
```
