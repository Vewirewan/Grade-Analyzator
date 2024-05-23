import tkinter as tk

def parse_fraction(fraction_str):
    parts = fraction_str.split('/')  
    if len(parts) != 2:
        raise ValueError("Неверный формат ")
    numerator = int(parts[0])
    denominator = int(parts[1])
    if denominator == 0:
        raise ValueError("Пропустите")
    return numerator, denominator

def calculate_grade():
    b_values = []
    for i in range(10):
        b_input = b_entries[i].get()
        if b_input:
            b_values.append(int(b_input))
        else:
            b_values.append(0)

    b10, b9, b8, b7, b6, b5, b4, b3, b2, b1 = b_values

    try:
        bjb1_input = bjb1_entry.get()
        bjb1_numerator, bjb1_denominator = parse_fraction(bjb1_input) if bjb1_input else (0, 0)
        bjb1min = min(bjb1_numerator, bjb1_denominator)
        bjb1max = max(bjb1_numerator, bjb1_denominator)

        bjb2_input = bjb2_entry.get()
        bjb2_numerator, bjb2_denominator = parse_fraction(bjb2_input) if bjb2_input else (0, 0)
        bjb2min = min(bjb2_numerator, bjb2_denominator)
        bjb2max = max(bjb2_numerator, bjb2_denominator)

        bjb3_input = bjb3_entry.get()
        bjb3_numerator, bjb3_denominator = parse_fraction(bjb3_input) if bjb3_input else (0, 0)
        bjb3min = min(bjb3_numerator, bjb3_denominator)
        bjb3max = max(bjb3_numerator, bjb3_denominator)

        bjb4_input = bjb4_entry.get()
        bjb4_numerator, bjb4_denominator = parse_fraction(bjb4_input) if bjb4_input else (0, 0)
        bjb4min = min(bjb4_numerator, bjb4_denominator)
        bjb4max = max(bjb4_numerator, bjb4_denominator)

        tjb_input = tjb_entry.get()
        tjb_numerator, tjb_denominator = parse_fraction(tjb_input) if tjb_input else (0, 0)
        tjbmin = min(tjb_numerator, tjb_denominator)
        tjbmax = max(tjb_numerator, tjb_denominator)
    except ValueError as e:
        result_label.config(text="Ошибка ввода : " + str(e))
        return

    x = ((b10 * 10) + (b9 * 9) + (b8 * 8) + bjb1min + bjb2min) / (bjb1max + bjb2max + ((b10 + b9 + b8) * 10)) * 100
    y = tjbmin / tjbmax * 100
    z = (x + y) / 2

    z_rounded = round(z)

    result_label.config(text=str(z_rounded) + "%")
    if z_rounded >= 85:
        grade_label.config(text="оценка за четверть 5")
    elif 65 <= z_rounded < 85:
        grade_label.config(text="оценка за четверть 4")
    elif 40 <= z_rounded < 65:
        grade_label.config(text="оценка за четверть 3")
    else:
        grade_label.config(text="оценка за четверть 2")

def reset():
    for entry in b_entries:
        entry.delete(0, tk.END)
    bjb1_entry.delete(0, tk.END)
    bjb2_entry.delete(0, tk.END)
    bjb3_entry.delete(0, tk.END)
    bjb4_entry.delete(0, tk.END)
    tjb_entry.delete(0, tk.END)
    result_label.config(text="")
    grade_label.config(text="")

root = tk.Tk()
root.title("Калькулятор оценки за четверть")

b_entries = []
for i in range(10):
    b_label = tk.Label(root, text=f"{10-i} баллов:")
    b_label.grid(row=i, column=0, padx=5, pady=5)
    b_entry = tk.Entry(root)
    b_entry.grid(row=i, column=1, padx=5, pady=5)
    b_entries.append(b_entry)

bjb1_label = tk.Label(root, text="CОР1:")
bjb1_label.grid(row=10, column=0, padx=5, pady=5)
bjb1_entry = tk.Entry(root)
bjb1_entry.grid(row=10, column=1, padx=5, pady=5)

bjb2_label = tk.Label(root, text="СОР2:")
bjb2_label.grid(row=11, column=0, padx=5, pady=5)
bjb2_entry = tk.Entry(root)
bjb2_entry.grid(row=11, column=1, padx=5, pady=5)

bjb3_label = tk.Label(root, text="СОР3:")
bjb3_label.grid(row=12, column=0, padx=5, pady=5)
bjb3_entry = tk.Entry(root)
bjb3_entry.grid(row=12, column=1, padx=5, pady=5)

bjb4_label = tk.Label(root, text="СОР4:")
bjb4_label.grid(row=13, column=0, padx=5, pady=5)
bjb4_entry = tk.Entry(root)
bjb4_entry.grid(row=13, column=1, padx=5, pady=5)

tjb_label = tk.Label(root, text="СОЧ:")
tjb_label.grid(row=14, column=0, padx=5, pady=5)
tjb_entry = tk.Entry(root)
tjb_entry.grid(row=14, column=1, padx=5, pady=5)

calculate_button = tk.Button(root, text="Рассчитать", command=calculate_grade)
calculate_button.grid(row=15, column=0, columnspan=2, padx=5, pady=5)

reset_button = tk.Button(root, text="Сбросить", command=reset)
reset_button.grid(row=15, column=1, padx=5, pady=5, sticky='e')

result_label = tk.Label(root, text="")
result_label.grid(row=16, column=0, columnspan=2, padx=5, pady=5)

grade_label = tk.Label(root, text="")
grade_label.grid(row=17, column=0, columnspan=2, padx=5, pady=5)

root.mainloop()

