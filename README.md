# Creating-A-Calculator-Using-Tkinter-Python-Tkinter









import tkinter as tk

class Calculator:
    def __init__(self, root):
        self.root = root
        self.root.title("Simple Calculator")

        self.entry = tk.Entry(root, width=16, font=('Arial', 24), borderwidth=2, relief="groove")
        self.entry.grid(row=0, column=0, columnspan=4)

        self.create_buttons()

    def create_buttons(self):
        buttons = [
            '7', '8', '9', '/',
            '4', '5', '6', '*',
            '1', '2', '3', '-',
            'C', '0', '=', '+'
        ]

        row_val = 1
        col_val = 0

        for button in buttons:
            command = lambda x=button: self.on_button_click(x)
            tk.Button(self.root, text=button, width=5, height=2, font=('Arial', 18), command=command).grid(row=row_val, column=col_val)
            col_val += 1
            if col_val > 3:
                col_val = 0
                row_val += 1

    def on_button_click(self, char):
        if char == 'C':
            self.entry.delete(0, tk.END)
        elif char == '=':
            try:
                result = eval(self.entry.get())
                self.entry.delete(0, tk.END)
                self.entry.insert(tk.END, str(result))
            except Exception as e:
                self.entry.delete(0, tk.END)
                self.entry.insert(tk.END, "Error")
        else:
            self.entry.insert(tk.END, char)

if __name__ == "__main__":
    root = tk.Tk()
    calculator = Calculator(root)
    root.mainloop()
