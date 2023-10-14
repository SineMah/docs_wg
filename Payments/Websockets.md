*Client Auth*

[[Payments]]

```async with websockets.connect(
    "wss://example.com",
    extra_headers={"Authorization": f"Bearer {token}"}
) as websocket:
    ...
