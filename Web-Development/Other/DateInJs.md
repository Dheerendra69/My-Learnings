### what is Date.toLocaleString()?

`Date.toLocaleString()` converts a `Date` object into a **human-readable date and time string**, formatted according to a **specific locale and formatting rules**.

### Syntax

```ts
date.toLocaleString(locales?, options?)
```

### What it does

* Formats **date + time**
* Uses **local conventions** (language, date order, separators, 12/24-hour clock)
* Adapts to the user’s **system or specified locale**

### Example

```ts
const d = new Date('2026-01-14T10:30:00Z');

d.toLocaleString();
// "14/1/2026, 4:00:00 PM" (India, IST)
// "1/14/2026, 10:30:00 AM" (US)
```

### With locale

```ts
d.toLocaleString('en-IN');
// "14/1/2026, 4:00:00 PM"
```

### With options

```ts
d.toLocaleString('en-IN', {
  year: 'numeric',
  month: 'long',
  day: '2-digit',
  hour: '2-digit',
  minute: '2-digit',
});
```

### Key points

* Locale-aware
* Timezone-aware (uses local timezone by default)
* Safer than manual date formatting
* Returns a **string**, not a `Date`

### Related methods

* `toLocaleDateString()` → date only
* `toLocaleTimeString()` → time only
