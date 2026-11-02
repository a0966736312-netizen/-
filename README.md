# -
程式相關作品
[python 尋寶探險.py](https://github.com/user-attachments/files/34255402/python.py)
# Kernel reset again — re-import and rerun everything
import matplotlib.pyplot as plt
import random
import seaborn as sns

# Set seaborn style
sns.set(style="whitegrid")

# 建立完整 6 副牌（312 張）
def build_deck():
    return [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10] * 24  # J/Q/K 視為 10 點

# 補牌到 17 停的模擬邏輯
def simulate_strategy_17(num_games=1000):
    full_deck = build_deck()
    results = []
    deck = full_deck[:]
    random.shuffle(deck)

    for _ in range(num_games):
        if len(deck) < 125:
            deck = build_deck()
            random.shuffle(deck)

        hand = [deck.pop(), deck.pop()]
        total = sum(hand)

        while total < 17 and deck:
            total += deck.pop()

        results.append(total)

    return results

# 執行模擬（補到 17 停，模擬 2000 局）
results_17 = simulate_strategy_17(2000)

# 繪製最終點數分布圖
plt.figure(figsize=(10, 6))
sns.histplot(results_17, bins=range(12, 32), kde=False, stat="count", color="skyblue", edgecolor="black")
plt.title("補牌策略：補到 17 點為止（2000 局模擬）\n莊家最終點數分布圖")
plt.xlabel("最終點數")
plt.ylabel("出現次數")
plt.xticks(range(12, 32))
plt.tight_layout()
plt.savefig("/mnt/data/strategy_17_distribution.png")

"/mnt/data/strategy_17_distribution.png"
