# Spring Boot

### Your `@Transactional` method is failing silently
- **Category:** Spring Boot / Proxies
- **Level:** Mid
- **Languages:** Java
- **Status:** Scripted
- **Video:** -

**Answer (draft):**

Spring implements transactions via proxies. An external caller goes through the proxy, the proxy opens the transaction, then calls your method. But when you call `this.update()` from another method in the same class, that call bypasses the proxy entirely. No proxy, no transaction.

Fix: move the transactional method to another bean, or use self-injection.

```java
// Broken: self-invocation bypasses proxy
@Service
public class OrderService {
    public void createOrder() {
        this.updateStock();  // no proxy, no tx
    }

    @Transactional
    public void updateStock() { ... }
}

// Fixed: call through another bean
@Service
public class OrderService {
    @Autowired private StockService stockService;

    public void createOrder() {
        stockService.updateStock();  // goes through proxy
    }
}
```

### Your `@Async` method still runs on the caller's thread. Why?
- **Category:** Spring Boot / Asynchronous Execution
- **Level:** Mid
- **Languages:** Java
- **Status:** Planned
- **Video:** -

### Your transaction committed even though a checked exception was thrown. Is that expected?
- **Category:** Spring Boot / Transactions
- **Level:** Mid
- **Languages:** Java
- **Status:** Planned
- **Video:** -

### Your endpoint executes one query, so why does Hibernate run hundreds more?
- **Category:** Spring Boot / JPA
- **Level:** Mid
- **Languages:** Java
- **Status:** Planned
- **Video:** -

### Does `@Transactional(readOnly = true)` prevent every database write?
- **Category:** Spring Boot / Transactions
- **Level:** Mid
- **Languages:** Java
- **Status:** Planned
- **Video:** -
