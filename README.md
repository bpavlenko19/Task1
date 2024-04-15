# Модуль Users

class User:
    def __init__(self, username, email, password):
        self.username = username
        self.email = email
        self.password = password
        self.subscriptions = []

    def subscribe(self, subscription):
        self.subscriptions.append(subscription)

    def __str__(self):
        return f"User: {self.username}, Email: {self.email}"


# Модуль Subscriptions

class Subscription:
    def __init__(self, name, price):
        self.name = name
        self.price = price

    def __str__(self):
        return f"Subscription: {self.name}, Price: {self.price}"


# Модуль Auth

class AuthService:
    def __init__(self):
        self.users = []

    def register_user(self, username, email, password):
        new_user = User(username, email, password)
        self.users.append(new_user)
        return new_user

    def login(self, email, password):
        for user in self.users:
            if user.email == email and user.password == password:
                return user
        return None


# Сценарій: Користувач підписується на нову послугу

if __name__ == "__main__":
    auth_service = AuthService()

    # Реєстрація користувача
    user1 = auth_service.register_user("user1", "user1@example.com", "password123")

    # Вхід користувача
    logged_in_user = auth_service.login("user1@example.com", "password123")

    if logged_in_user:
        print("Вхід успішний:", logged_in_user)
    else:
        print("Помилка входу. Перевірте дані.")

    # Створення підписки
    subscription1 = Subscription("Premium", 9.99)

    # Підписка користувача
    user1.subscribe(subscription1)

    print(user1.subscriptions)
