# 🚀 FastAPI Item Processing API

This is a simple **FastAPI** application that processes and validates `Item` objects sent via POST requests. The API ensures the item data is correctly formatted and appends a unique identifier (UUID) to each valid item.

---

## 📦 Requirements

Make sure you have FastAPI and Uvicorn installed:

```bash
pip install fastapi uvicorn
```

---

## 🚀 Running the Server

To run the application locally:

```bash
uvicorn main:app --reload
```

> Replace `main` with the filename of your Python script (without `.py`).

---

## 📄 Endpoint

### `POST /processar-item`

Processes and validates an item. If the data is valid, it returns the same item along with a generated `uuid`.

#### 🔸 Request Body

```json
{
  "nome": "Example Item",
  "valor": 99.99,
  "data": "2024-04-25"
}
```

#### 🔹 Field Validations

- `nome`: Required, max 25 characters.
- `valor`: Required, float.
- `data`: Required, must be in `YYYY-MM-DD` format and **not in the future**.

#### ✅ Successful Response

```json
{
  "nome": "Example Item",
  "valor": 99.99,
  "data": "2024-04-25",
  "uuid": "b91eb4c1-5a25-41a2-b2a0-2f708d3a2fae"
}
```

#### ❌ Validation Errors

Examples of invalid input will trigger error responses, such as:

```json
{
  "detail": [
    {
      "loc": ["body", "data"],
      "msg": "The date must not be in the future.",
      "type": "value_error"
    }
  ]
}
```

---

## ⚙️ Code Overview

- `Item` model uses **Pydantic** for data validation.
- Custom validation ensures that:
  - The `nome` field is not too long.
  - The `data` is properly formatted and not a future date.
- A UUID is generated using `uuid4()` and appended to the returned dictionary.

---

## 📌 Notes

- This app is ideal for quickly testing structured validation with FastAPI.
- The structure can be extended to support databases, authentication, and more.
