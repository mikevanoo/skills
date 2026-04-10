# When to Mock

Mock at **system boundaries** only:

- External APIs (payment, email, etc.)
- Databases (sometimes - prefer test DB)
- Time/randomness
- File system (sometimes)

Don't mock:

- Your own classes/modules
- Internal collaborators
- Anything you control

## Designing for Mockability

At system boundaries, design interfaces that are easy to mock:

**1. Use dependency injection**

Pass external dependencies in rather than creating them internally:

**TypeScript:**
```typescript
// Easy to mock
function processPayment(order, paymentClient) {
  return paymentClient.charge(order.total);
}

// Hard to mock
function processPayment(order) {
  const client = new StripeClient(process.env.STRIPE_KEY);
  return client.charge(order.total);
}
```

**C#:**
```csharp
// Easy to mock
decimal ProcessPayment(Order order, IPaymentClient paymentClient) {
  return paymentClient.Charge(order.Total);
}

// Hard to mock
decimal ProcessPayment(Order order) {
  var client = new StripeClient(Environment.GetEnvironmentVariable("STRIPE_KEY"));
  return client.Charge(order.Total);
}
```

**2. Prefer SDK-style interfaces over generic fetchers**

Create specific functions for each external operation instead of one generic function with conditional logic:

**TypeScript:**
```typescript
// GOOD: Each function is independently mockable
const api = {
  getUser: (id) => fetch(`/users/${id}`),
  getOrders: (userId) => fetch(`/users/${userId}/orders`),
  createOrder: (data) => fetch('/orders', { method: 'POST', body: data }),
};

// BAD: Mocking requires conditional logic inside the mock
const api = {
  fetch: (endpoint, options) => fetch(endpoint, options),
};
```

**C#:**
```csharp
// GOOD: Each method is independently mockable
public interface IApiClient {
  User GetUser(int id);
  List<Order> GetOrders(int userId);
  Order CreateOrder(OrderData data);
}

// BAD: Mocking requires conditional logic inside the mock
public interface IApiClient {
  HttpResponseMessage Fetch(string endpoint, HttpRequestMessage options);
}
```

The SDK approach means:
- Each mock returns one specific shape
- No conditional logic in test setup
- Easier to see which endpoints a test exercises
- Type safety per endpoint
