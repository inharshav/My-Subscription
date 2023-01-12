# My-Subscription
import itertools

class NewspaperSubscription:
    def __init__(self, name, daily_price):
        self.name = name
        self.daily_price = daily_price
        self.weekly_price = daily_price * 7

    def __str__(self):
        return f"{self.name}: INR {self.weekly_price}/week"

subscriptions = [
    NewspaperSubscription("Times of India", 5),
    NewspaperSubscription("Hindustan Times", 6),
    NewspaperSubscription("Economic Times", 10),
    NewspaperSubscription("The Hindu", 8)
]

def get_combinations(subscriptions, budget, index=0):
    if index == len(subscriptions):
        return [[]]
    else:
        current_sub = subscriptions[index]
        combinations = []
        for i in range(0, int(budget/current_sub.weekly_price) + 1):
            for comb in get_combinations(subscriptions, budget - i*current_sub.weekly_price, index+1):
                combinations.append([(current_sub, i)] + comb)
        return combinations

def generate_combinations(subscriptions, budget):
    all_combinations = get_combinations(subscriptions, budget)
    valid_combinations = [comb for comb in all_combinations if sum(sub.weekly_price*count for sub, count in comb) == budget]
    return valid_combinations

budget = int(input("Enter your weekly budget for subscriptions: "))
combinations = generate_combinations(subscriptions, budget)
for comb in combinations:
    print(comb)
