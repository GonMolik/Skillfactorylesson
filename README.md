field = [[" "] * 3 for i in range(3)]


def show():
    print()
    print("   | 0 | 1 | 2 | ")
    print(" -------------- ")
    for i, row in enumerate(field):
        row_str = f" {i} | {' | '.join(row)} | "
        print(row_str)
        print(" -------------- ")


def ask():
    while True:
        try:
            x, y = map(int, input("Ваш ход (строка столбец): ").split())

            if 0 > x or x > 2 or 0 > y or y > 2:
                print("Координаты вне диапазона (0-2)")
                continue

            if field[x][y] != " ":
                print("Клетка занята")
                continue

            return x, y

        except ValueError:
            print("Введите два числа через пробел")


def check_win(player):
    # Проверка строк
    for row in field:
        if all(cell == player for cell in row):
            return True

    # Проверка столбцов
    for col in range(3):
        if all(field[row][col] == player for row in range(3)):
            return True

    # Проверка диагоналей
    if all(field[i][i] == player for i in range(3)) or \
            all(field[i][2 - i] == player for i in range(3)):
        return True

    return False


def game():
    current_player = "X"
    step = 1

    while True:
        show()
        print(f"Ход игрока {current_player}")
        x, y = ask()
        field[x][y] = current_player

        if check_win(current_player):
            show()
            print(f"Игрок {current_player} победил!")
            break

        if step == 9:
            show()
            print("Ничья!")
            break

        current_player = "O" if current_player == "X" else "X"
        step += 1


print("Вводите координаты через пробел (например: 1 2)")
print("Первое число - строка, второе - столбец (0-2)")
game()
