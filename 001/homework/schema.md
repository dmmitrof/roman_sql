Что изменилось и почему:

quantity, price, product ушли из orders → в order_items. Теперь один заказ может содержать несколько товаров — это реальность любого магазина.

orders стал «шапкой заказа»: кто, где, когда. Сумма заказа считается через order_items (это будет тема одного из следующих уроков — SUM + GROUP BY).

stores — таблица с магазинами. Даёт естественный второй JOIN и красивый вопрос «в каком магазине больше заказов».

customer_id и store_id в orders — два FK, два разных JOIN. Отлично для практики.

Новая схема:

    customers                          orders                         stores
    ┌──────────────────┐              ┌──────────────────────┐      ┌──────────────────┐
    │ customer_id  PK  │◄─────────────│ order_id       PK    │      │ store_id    PK   │
    │ name             │              │ customer_id    FK    │      │ store_name       │
    │ city             │              │ store_id       FK    │─────►│ city             │
    │ signup_date      │              │ order_date           │      │ opened_date      │
    └──────────────────┘              └──────────┬───────────┘      └──────────────────┘
                                                 │
                                                 │ 1 : N
                                                 ▼
                                    ┌──────────────────────────┐
                                    │ order_items              │
                                    │──────────────────────────│
                                    │ order_item_id  PK        │
                                    │ order_id       FK        │
                                    │ product                  │
                                    │ quantity                 │
                                    │ price                    │
                                    └──────────────────────────┘
