---
layout: layout.njk
title: A good router!
---

# Intro

Goodrouter is a router implemented in two languages, TypeScript and Rust. The router is simple and supports parsing and formatting of routes. It can be used in any environment, in a client or server. The router uses a trie-ish data structure that makes the router scalable and fast.

It's a good router!

## TypeScript

```typescript
const router = new Router();

router.insertRoute("all-products", "/product/all");
router.insertRoute("product-detail", "/product/{id}");

// And now we can parse routes!

{
  const route = router.parseRoute("/not-found");
  assert.equal(route, null);
}

{
  const route = router.parseRoute("/product/all");
  assert.deepEqual(route, {
    name: "all-products",
    parameters: {},
  });
}

{
  const route = router.parseRoute("/product/1");
  assert.deepEqual(route, {
    name: "product-detail",
    parameters: {
      id: "1",
    },
  });
}

// And we can stringify routes

{
  const path = router.stringifyRoute({
    name: "all-products",
    parameters: {},
  });
  assert.equal(path, "/product/all");
}

{
  const path = router.stringifyRoute({
    name: "product-detail",
    parameters: {
      id: "2",
    },
  });
  assert.equal(path, "/product/2");
}
```

## Rust

```rust
let mut router = Router::new();

router.insert_route("all-products", "/product/all");
router.insert_route("product-detail", "/product/{id}");

// And now we can parse routes!

{
  let route = router.parse_route("/not-found".to_owned(),);
  assert_eq!(route, None);
}

{
  let route = router.parse_route("/product/all".to_owned(),);
  assert_eq!(route, Some(Route{
    name: "all-products".to_owned(),
    parameters: vec![],
  }));
}

{
  let route = router.parse_route("/product/1".to_owned(),);
  assert_eq!(route, Some(Route{
    name: "product-detail".to_owned(),
    parameters: vec![
      ("id", "1"),
    ],
  }));
}

// And we can stringify routes

{
  let path = router.stringify_route(Some(Route{
    name: "all-products".to_owned(),
        parameters: vec![],
  }));
  assert_eq!(path, "/product/all".to_owned(),);
}

{
  let path = router.stringify_route(Some(Route{
    name: "product-detail".to_owned(),
    parameters: vec![
      ("id", "1"),
    ],
  }));
  assert_eq!(path, "/product/2".to_owned());
}
```
