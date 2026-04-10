# Good and Bad Tests

## Good Tests

**Integration-style**: Test through real interfaces, not mocks of internal parts.

**TypeScript:**
```typescript
// GOOD: Tests observable behavior
test("user can checkout with valid cart", async () => {
  const cart = createCart();
  cart.add(product);
  const result = await checkout(cart, paymentMethod);
  expect(result.status).toBe("confirmed");
});
```

**C# (xUnit + AwesomeAssertions):**
```csharp
// GOOD: Tests observable behavior
[Fact]
public async Task UserCanCheckoutWithValidCart()
{
    var cart = CreateCart();
    cart.Add(product);
    var result = await Checkout(cart, paymentMethod);
    result.Status.Should().Be("confirmed");
}
```

Characteristics:

- Tests behavior users/callers care about
- Uses public API only
- Survives internal refactors
- Describes WHAT, not HOW
- One logical assertion per test

## Bad Tests

**Implementation-detail tests**: Coupled to internal structure.

**TypeScript:**
```typescript
// BAD: Tests implementation details
test("checkout calls paymentService.process", async () => {
  const mockPayment = jest.mock(paymentService);
  await checkout(cart, payment);
  expect(mockPayment.process).toHaveBeenCalledWith(cart.total);
});
```

**C# (xUnit + NSubstitute):**
```csharp
// BAD: Tests implementation details
[Fact]
public async Task CheckoutCallsPaymentServiceProcess()
{
    var mockPayment = Substitute.For<IPaymentService>();
    await Checkout(cart, mockPayment);
    mockPayment.Received().Process(cart.Total);
}
```

Red flags:

- Mocking internal collaborators
- Testing private methods
- Asserting on call counts/order
- Test breaks when refactoring without behavior change
- Test name describes HOW not WHAT
- Verifying through external means instead of interface

**TypeScript:**
```typescript
// BAD: Bypasses interface to verify
test("createUser saves to database", async () => {
  await createUser({ name: "Alice" });
  const row = await db.query("SELECT * FROM users WHERE name = ?", ["Alice"]);
  expect(row).toBeDefined();
});

// GOOD: Verifies through interface
test("createUser makes user retrievable", async () => {
  const user = await createUser({ name: "Alice" });
  const retrieved = await getUser(user.id);
  expect(retrieved.name).toBe("Alice");
});
```

**C# (xUnit + AwesomeAssertions):**
```csharp
// BAD: Bypasses interface to verify
[Fact]
public async Task CreateUserSavesToDatabase()
{
    await CreateUser(new { Name = "Alice" });
    var row = await db.Query("SELECT * FROM users WHERE name = @name", new { name = "Alice" });
    row.Should().NotBeNull();
}

// GOOD: Verifies through interface
[Fact]
public async Task CreateUserMakesUserRetrievable()
{
    var user = await CreateUser(new { Name = "Alice" });
    var retrieved = await GetUser(user.Id);
    retrieved.Name.Should().Be("Alice");
}
```
