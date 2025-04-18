## Anhor Korxonasining ishchilar davomatini olib boruvchi loyiha

1. **Product** - (Maxsulotlar)
    * ``name`` - Maxsulot nomi
    * ``price_per_unit`` - 1 dona chiqaril maxsulot uchun tolanadigan summa.
1. **Special Product** - (Maxsus Maxsulotlar)
    * ``name`` - Maxsulot nomi
    * ``price_per_unit`` - 1 dona chiqaril maxsulot uchun tolanadigan summa.
2. **Employee** - (Ishchilar)
    * ``status`` - Ishchi statusi yani (``yangi``, ``doimiy`` ``...``)
    * ``full_name`` - Ishchining ``Ism familiasi``
    * ``is_busy`` - Ishchining ishga kelgan va kelmaganligini filterlash uchun
3. **Daily Production** - (Kunlik ishlab chiqarish)
    * ``date`` - Sana yani qaysi kunga tegishli ekanligi
    * ``product`` - Mahsulot
    * ``quantity`` - Mahsulot chiqarilgan soni
    * ``total_amount`` - To'lanadigan summa ``avtomatik hisoblanadi``

3. **Daily Special Production** - (Kunlik ishlab chiqarish)
    * ``date`` - Sana yani qaysi kunga tegishli ekanligi
    * ``employee`` - ishchi
    * ``product`` - Mahsulot
    * ``quantity`` - Mahsulot chiqarilgan soni
    * ``total_amount`` - To'lanadigan summa ``avtomatik hisoblanadi``


4. **Attendance** - (Ishchilar davomati)
    * ``employee`` - Ishchi
    * ``check_in`` - Kelish vaqti
    * ``check_out`` - Ketish vaqti
    * ``worked_hours`` - kun davomida ishlagan vaqti (``Avtomatik hisoblanadi``)
    * ``break_time`` - Vaqtinchalik tanaffus oladigan bolsa (``default 0``)

* ``requirements.txt`` Loyiha uchun kerakli **package**lar.

      pip install -r requirements.txt

## Api ``Qo'llanma``

<br>

| Method   | Description                                                                                    |
|----------|------------------------------------------------------------------------------------------------|
| `GET`    | Bitta element yoki elementlar to'plamini olish uchun ishlatiladi.                              |
| `POST`   | Yangi narsalarni yaratishda foydalaniladi, masalan: yangi ishchi, maxsulot ...                 |
| `PATCH`  | Elementdagi bir yoki bir nechta maydonlarni yangilash uchun ishlatiladi.                       |
| `PUT`    | Butun elementni (barcha maydonlarni) yangi ma'lumotlar bilan almashtirish uchun foydalaniladi. |
| `DELETE` | Elementni o'chirish uchun ishlatiladi.                                                         |

<br>

| Method   | URL                                         | Description                           |
|----------|---------------------------------------------|---------------------------------------|
| `GET`    | `/api/v1/employee`                          | Barcha ishchilarni olish.             |
| `POST`   | `/api/v1/employee`                          | Yangi ishchi yaratish.                |
| `GET`    | `/api/v1/employee/28`                       | №28 ishchini olish.                   |
| `PATCH`  | `/api/v1/employee/28`                       | Ishchini ma'lumotlarni yangilash #28. |
| `DELETE` | `/api/v1/employee/28` or `/api/employee/50` | Ishchini o'chirish                    |

<br>
<br>

## HTTP javob holati kodlari

Bu API ishlatayotganda server tomonidan qaytariladigan muhim status xabarlaridir. Har bir kod ma'lum bir holatni
bildiradi va tushunish oson bo'lishi uchun turlarga bo'lingan.

### Asosiy HTTP Status Kodlari:

| Code  | Title                   | Description                                                                                   |
|-------|-------------------------|-----------------------------------------------------------------------------------------------|
| `200` | `OK`                    | So'rov muvaffaqiyatli bajarildi (masalan. foydalanganda `GET`, `PATCH`, `PUT` yoki `DELETE`). |
| `201` | `Created`               | Yangi resurs yaratildi (masalan, POST so'rovi orqali).                                        |
| `400` | `Bad request`           | So'rov noto'g'ri yuborilgan (masalan, majburiy maydonlar yo'q)                                |
| `401` | `Unauthorized`          | Foydalanuvchi avtorizatsiyadan o'tmagan.                                                      |
| `403` | `Forbidden`             | Foydalanuvchiga ruxsat yo'q (avtorizatsiyadan o'tgan bo'lsa ham).                             |
| `404` | `Not found`             | So'ralgan resurs topilmadi.                                                                   |
| `500` | `Internal server error` | Serverda kutilmagan xato yuz berdi.                                                           |
| `502` | `Bad Gateway`           | Gateway yoki proxy server noto'g'ri javob qaytardi.                                           |
| `503` | `Service Unavailable`   | Server hozircha ishlamayapti (vaqtincha).                                                     |

<br>
<br>
<br>

### Employee example

* ``Post method``

       {
           "status": "yangi",
           "full_name": "Temirov Muhammad"
       }

* ``Get method``

      {
          "count": 2,
          "next": null,
          "previous": null,
          "results": [
              {
                  "id": 1,
                  "status": "yangi",
                  "name": "Muhammad"
              },
              {
                  "id": 2,
                  "status": "doimiy",
                  "name": "Muhammadali"
              }
       ]
      }


### Product and Special Product example
* ``Post method``

      {
        "name": "To'yona 1 Litr",
        "price_per_unit" : "500"
      }

* ``Get method``

      [
        {
            "id": 1,
            "name": "To'yona 1 Litr",
            "price_per_unit": "500.00"
        },
        {
            "id": 1,
            "name": "To'yona 2 Litr",
            "price_per_unit": "900.00"
        }
      ]

### Daily Production example

* ``Post method``

       {
         "date": "2025-03-24",
         "product": 4,
         "quantity": 1000
       }

* ``Get method``

      {
        "count": 3,
        "next": null,
        "previous": null,
        "results": [
          {
              "id": 3,
              "product_name": "Xo'jaili 12 talik",
              "date": "2025-04-17",
              "quantity": 500,
              "total_amount": "660000.00",
              "product": 5
          },
          {
              "id": 2,
              "product_name": "0.9 - 6 talik",
              "date": "2025-04-17",
              "quantity": 100,
              "total_amount": "66000.00",
              "product": 2
          },
          {
              "id": 1,
              "product_name": "To'yona 1 Litr",
              "date": "2025-04-17",
              "quantity": 1000,
              "total_amount": "960000.00",
              "product": 1
          }
        ]
      }


### Daily Special Product

* ``Post method``
        
      {
        "date": "2025-04-02",
        "employee": 1,
        "product": 1,
        "quantity": 100
      }

* ``Get method``

      {
        "count": 1,
        "next": null,
        "previous": null,
        "results": [
            {
                "id": 1,
                "product_name": "1 Litr",
                "date": "2025-04-17",
                "quantity": 1000,
                "total_amount": "140000.00",
                "employee": 1,
                "product": 1
            }
        ]
      }

### Filter daily products by date

* ``post method``

      {
        "start_date": "2025-04-01"
      }
             Yoki
      {
        "start_date": "2025-04-01",
        "end_date": "2025-04-20"
      }


* ``Response``

      [
        {
            "id": 2,
            "product_name": "1 Litr",
            "date": "2025-04-02",
            "quantity": 100,
            "total_amount": "14000.00",
            "employee": 1,
            "product": 1
        },
        {
            "id": 3,
            "product_name": "1 Litr",
            "date": "2025-04-02",
            "quantity": 100,
            "total_amount": "14000.00",
            "employee": 2,
            "product": 1
        },
        {
            "id": 1,
            "product_name": "1 Litr",
            "date": "2025-04-17",
            "quantity": 1000,
            "total_amount": "140000.00",
            "employee": 1,
            "product": 1
        }
      ]

### Attendance check In example

* ``Post method``

       {
          "check_in": "2025-04-16T09:00:00",
          "employees": [1,2,3]
       }

* ``Get method``

      [
        {
            "id": 2,
            "name": "Jahongir"
        },
        {
            "id": 1,
            "name": "Muhammadali"
        },
        {
            "id": 3,
            "name": "Sarvinoz"
        },
        {
            "id": 4,
            "name": "Umida"
        }
      ]

### Attendance check out example

* ``Post method``

      {
          "check_out": "2025-04-16T09:00:00",
          "employees": [1,2,3]
      }

* ``Get method``

      [
        {
            "id": 2,
            "name": "Jahongir"
        },
        {
            "id": 1,
            "name": "Muhammadali"
        },
        {
            "id": 3,
            "name": "Sarvinoz"
        }
      ]

### Daily Attendance

* ``Post method``

      {
        "date": "2025-04-16"
      }
* ``Response``
  
      [
        {
            "id": 8,
            "check_in": "2025-04-16T09:00:00+05:00",
            "check_out": "2025-04-16T19:00:00+05:00",
            "worked_hours": "8.50",
            "break_time": "1.50",
            "employee": 1
        },
        {
            "id": 10,
            "check_in": "2025-04-16T09:00:00+05:00",
            "check_out": "2025-04-16T19:30:00+05:00",
            "worked_hours": "10.50",
            "break_time": "0.00",
            "employee": 2
        },
        {
            "id": 11,
            "check_in": "2025-04-16T09:00:00+05:00",
            "check_out": "2025-04-16T19:30:00+05:00",
            "worked_hours": "10.50",
            "break_time": "0.00",
            "employee": 1
        },
        {
            "id": 12,
            "check_in": "2025-04-16T09:00:00+05:00",
            "check_out": "2025-04-16T19:00:00+05:00",
            "worked_hours": "10.00",
            "break_time": "0.00",
            "employee": 3
        }
      ]
  
