# validator

Checks for user input such as web forms: e-mail, URL, phone, dates, passwords, lengths and ranges, and a simple way to collect error messages.

فحص مدخلات المستخدم مثل نماذج الويب: البريد الإلكتروني، والروابط، والهواتف، والتواريخ، وكلمات المرور، والأطوال والنطاقات، وطريقة بسيطة لجمع رسائل الأخطاء.

Requires Elomar-Lang 0.2.0 or later.

## Install

```text
elomar add validator
```

or in `elomar.toml`:

```toml
[dependencies]
validator = "0.1"
```

## Use

```elomar
use validator.check

fn main() {
    let name = "L"
    let email = "lina@example.com"
    let problems = check.collect([
        check.require(check.length_between(name, 2, 50), "name is too short"),
        check.require(check.email(email), "email is not valid")
    ])
    print(problems)                                // ["name is too short"]
    print(check.iso_date("2024-02-29"))            // true
    print(check.strong_password("Secret123"))      // true
}
```

| Function (`check.…`) | |
|---|---|
| `email(s) -> Bool` | `text@domain.tld`, no spaces |
| `url(s) -> Bool` | `http://` or `https://` with a host |
| `phone(s) -> Bool` | optional `+` and 7–15 digits; spaces, `-`, `.` and `()` allowed |
| `digits(s) -> Bool` | only 0–9 |
| `iso_date(s) -> Bool` | `YYYY-MM-DD` that exists in the calendar |
| `strong_password(s) -> Bool` | 8+ letters with lower case, upper case and a digit |
| `length_between(s, min, max) -> Bool` | letter count in range |
| `between(n, min, max) -> Bool` | number in range |
| `require(ok, message) -> Option<String>` | a rule: `None` when `ok` |
| `collect(rules) -> List<String>` | the messages of the rules that failed |

## بالعربية

ثبّت الحزمة بالأمر `elomar add validator`، ثم استوردها بـ `use validator.check`. الأمثلة
والدوال أعلاه تعمل كما هي، والحزمة تحتاج Elomar-Lang 0.2.0 أو أحدث.

## Development

```text
elomar test
elomar fmt --check .
```

## License

MIT or Apache-2.0, at your option.
