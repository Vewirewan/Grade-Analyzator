def parse_fraction(fraction_str):
    parts = fraction_str.split('/')  
    if len(parts) != 2:
        raise ValueError("Неверный формат ")
    numerator = int(parts[0])
    denominator = int(parts[1])
    if denominator == 0:
        raise ValueError("Пропустите")
    return numerator, denominator

while True:
    b_values = []
    for i in range(10):
        b_input = input(f"{10-i} баллов : ")
        if b_input:
            b_values.append(int(b_input))
        else:
            b_values.append(0)

    b10, b9, b8, b7, b6, b5, b4, b3, b2, b1 = b_values

    try:
        bjb1_input = input("CОР1: ")
        bjb1_numerator, bjb1_denominator = parse_fraction(bjb1_input) if bjb1_input else (0, 0)
        bjb1min = min(bjb1_numerator, bjb1_denominator)
        bjb1max = max(bjb1_numerator, bjb1_denominator)

        bjb2_input = input("СОР2: ")
        bjb2_numerator, bjb2_denominator = parse_fraction(bjb2_input) if bjb2_input else (0, 0)
        bjb2min = min(bjb2_numerator, bjb2_denominator)
        bjb2max = max(bjb2_numerator, bjb2_denominator)

        bjb3_input = input("СОР3: ")
        bjb3_numerator, bjb3_denominator = parse_fraction(bjb3_input) if bjb3_input else (0, 0)
        bjb3min = min(bjb3_numerator, bjb3_denominator)
        bjb3max = max(bjb3_numerator, bjb3_denominator)

        bjb4_input = input("СОР4: ")
        bjb4_numerator, bjb4_denominator = parse_fraction(bjb4_input) if bjb4_input else (0, 0)
        bjb4min = min(bjb4_numerator, bjb4_denominator)
        bjb4max = max(bjb4_numerator, bjb4_denominator)

        tjb_input = input("СОЧ: ")
        tjb_numerator, tjb_denominator = parse_fraction(tjb_input) if tjb_input else (0, 0)
        tjbmin = min(tjb_numerator, tjb_denominator)
        tjbmax = max(tjb_numerator, tjb_denominator)
    except ValueError as e:
        print("Ошибка ввода :", e)
        continue

    x = ((b10 * 10) + (b9 * 9) + (b8 * 8) + bjb1min + bjb2min) / (bjb1max + bjb2max + ((b10 + b9 + b8) * 10)) * 100
    y = tjbmin / tjbmax * 100
    z = (x + y) / 2

    z_rounded = round(z)


    print(str(z_rounded) + "%")
    if z_rounded >= 85:
        print("оценка за четверть 5")
    elif 65 <= z_rounded < 85:
        print("оценка за четверть 4")
    elif 40 <= z_rounded < 65:
        print("оценка за четверть 3")
    else:
        print("оценка за четверть 2")
        
    exit_command = input("Введите «exit», чтобы выйти, или нажмите Enter, чтобы продолжить.: ")
    if exit_command.lower() == 'exit':
        break


