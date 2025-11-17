# Опис сутностей 
## Presentation Layer

Web UI
— Інтерфейс, через який користувач здійснює пошук рейсів, створює бронювання, оплачує.

Mobile App (опційно)
— Альтернативний інтерфейс для взаємодії з сервісами.

## Business Logic Layer

UserService
— Логіка реєстрації, входу, отримання профілю.

FlightService
— Пошук рейсів, перевірка доступності місць.

ReservationService
— Створення бронювань, відміна, отримання квитків.

PaymentService
— Перевірка оплати, обробка транзакцій.

## Data Access Layer

Repositories (UserRepository, FlightRepository, ReservationRepository, PaymentRepository)
— Реалізують CRUD-операції з базою даних.

Database
— Зовнішній компонент, де зберігаються всі дані.

# Пояснення взаємодії
## 1. Presentation Layer => Business Logic Layer

UI не працює з даними напряму.
Він надсилає запити до сервісів рівня логіки:

Web UI викликає FlightService для пошуку рейсів.

Під час бронювання UI викликає ReservationService.

Для оплати — PaymentService.

UI не знає, як дані зберігаються — тільки виконує запити.

## 2. Business Logic Layer => Data Access Layer

Сервіси логіки працюють із репозиторіями:

FlightService звертається до FlightRepository

ReservationService — до ReservationRepository

PaymentService — до PaymentRepository

Сервіси реалізують бізнес-правила:
наприклад, “не можна створити бронювання, якщо немає доступних місць”.

## 3. Data Access Layer => Database

Репозиторії виконують:

SQL запити

збереження об’єктів

оновлення статусів

транзакції

База даних не знає нічого про логіку системи — вона просто зберігає дані.
