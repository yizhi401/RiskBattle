import random
import tkinter as tk


def risk_battle(attacker_count, defender_count):
    """进行一次Risk大战役战斗"""
    # 检查进攻方是否可以派出3个军队
    if attacker_count <= 1:
        return attacker_count, defender_count

    if defender_count <= 0:
        return attacker_count, defender_count

    # 进攻方派出3个军队
    if attacker_count >= 3:
        attacker_dice = sorted([random.randint(1, 6) for _ in range(3)], reverse=True)
    else:
        attacker_dice = sorted([random.randint(1, 6) for _ in range(attacker_count)], reverse=True)

    # 防守方派出至多2个军队
    if defender_count >= 2:
        defender_dice = sorted([random.randint(1, 6) for _ in range(2)], reverse=True)
    else:
        defender_dice = sorted([random.randint(1, 6) for _ in range(1)], reverse=True)

    # 进攻方选择同等数量的骰子进行对比
    for i in range(min(len(attacker_dice), len(defender_dice))):
        if attacker_dice[i] > defender_dice[i]:
            defender_count -= 1
        else:
            attacker_count -= 1

    return attacker_count, defender_count


class RiskBattleGUI:
    def __init__(self, master):
        self.master = master
        master.title("Risk 大战役")

        # 设置窗口尺寸和字体大小
        self.master.geometry("800x600")
        self.master.resizable(False, False)
        self.font_size = 24
        self.battle_count = 0

        # 创建标签和输入框
        self.label_attacker = tk.Label(master, text="进攻方军队数量:", font=("Arial", self.font_size))
        self.label_attacker.grid(row=0, column=0, padx=20, pady=20)
        self.entry_attacker = tk.Entry(master, font=("Arial", self.font_size), width=10)
        self.entry_attacker.grid(row=0, column=1, padx=20, pady=20)

        self.label_defender = tk.Label(master, text="防守方军队数量:", font=("Arial", self.font_size))
        self.label_defender.grid(row=1, column=0, padx=20, pady=20)
        self.entry_defender = tk.Entry(master, font=("Arial", self.font_size), width=10)
        self.entry_defender.grid(row=1, column=1, padx=20, pady=20)

        # 创建开始战斗按钮
        self.button_start = tk.Button(master, text="开始战斗", font=("Arial", self.font_size),
                                      command=self.start_battle)
        self.button_start.grid(row=2, column=0, columnspan=2, padx=20, pady=20)

        # 创建开始战斗按钮
        self.button_clean = tk.Button(master, text="打扫战场", font=("Arial", self.font_size),
                                      command=self.clean_battle)
        self.button_clean.grid(row=2, column=2, columnspan=2, padx=20, pady=20)

        # 创建结果显示标签
        self.text_result = tk.Text(master, font=("Arial", 12), height=10, width=80)
        self.text_result.grid(row=3, column=0, columnspan=3, padx=20, pady=20, sticky="nsew")

        # 设置窗口的行列权重,使text_result框铺满下半部分
        self.master.grid_rowconfigure(3, weight=1)
        self.master.grid_columnconfigure(0, weight=1)
        self.master.grid_columnconfigure(1, weight=1)
        self.master.grid_columnconfigure(2, weight=1)

    def clean_battle(self):
        self.battle_count = 0
        self.entry_attacker.delete(0, tk.END)
        self.entry_defender.delete(0, tk.END)
        self.text_result.delete(1.0, tk.END)

    def start_battle(self):
        # 获取用户输入的进攻方和防守方数量
        attacker_count = int(self.entry_attacker.get())
        defender_count = int(self.entry_defender.get())
        if attacker_count <= 1:
            self.text_result.insert(tk.END, f"\n战斗结束 - 进攻方失败!")
            return
        elif defender_count <= 0:
            self.text_result.insert(tk.END, f"\n战斗结束 - 进攻方胜利!")
            return

        self.battle_count += 1
        attacker_count, defender_count = risk_battle(attacker_count, defender_count)
        # 更新进攻方和防守方的输入框
        self.entry_attacker.delete(0, tk.END)
        self.entry_attacker.insert(0, str(attacker_count))
        self.entry_defender.delete(0, tk.END)
        self.entry_defender.insert(0, str(defender_count))
        self.text_result.insert(tk.END,
                                f"\n第{self.battle_count}次战斗 - 进攻方剩余: {attacker_count}, 防守方剩余: {defender_count}")

        self.master.update()


root = tk.Tk()
risk_gui = RiskBattleGUI(root)
root.mainloop()
