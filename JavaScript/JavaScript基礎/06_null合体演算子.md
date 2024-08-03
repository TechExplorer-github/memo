# null 合体演算子

null 合体演算子(??)は、論理演算子の一種で、左辺が null または undefined のときに右辺の値を返し、それ以外の場合は左辺の値を返す機能を持っています。

```typescript
const result1 = null ?? "default";
console.log(result1); // "default"

const result2 = 0 ?? "default";
console.log(result2); // 0
```

オプショナルチェーン演算子と null 合体演算子を組み合わせることで、プロパティが undefined または null の場合のデフォルト値を簡単に指定できます。

```typescript
const person = {
  name: "John",
  profile: {
    age: 20,
  }
};

const age = person.profile?.age ?? "unknown";
console.log(age) // 20

const gender = person.profile?gender ?? "unknown";
console.log(gender) // "unknown"
```
