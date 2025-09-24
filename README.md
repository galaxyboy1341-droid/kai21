import random

# Daftar ular dan tangga (posisi_awal: posisi_akhir)
snakes = {16: 6, 47: 26, 49: 11, 56: 53, 62: 19, 64: 60, 87: 24, 93: 73, 95: 75, 98: 78}
ladders = {1: 38, 4: 14, 9: 31, 21: 42, 28: 84, 36: 44, 51: 67, 71: 91, 80: 100}

def roll_dice():
    return random.randint(1, 6)

def move_player(player, position):
    input(f"\nGiliran {player}, tekan ENTER untuk melempar dadu...")
    dice = roll_dice()
    print(f"{player} melempar dadu dan mendapatkan angka {dice}")
    position += dice
    if position > 100:
        position = 100 - (position - 100)  # bounce back
    print(f"{player} bergerak ke kotak {position}")

    if position in snakes:
        print(f"Oh tidak! {player} digigit ular! Turun ke {snakes[position]}")
        position = snakes[position]
    elif position in ladders:
        print(f"Hore! {player} naik tangga! Naik ke {ladders[position]}")
        position = ladders[position]

    print(f"{player} sekarang di kotak {position}")
    return position

def main():
    print("=== Permainan Ular Tangga ===")
    print("Pemain 1 vs Pemain 2")
    positions = {"Pemain 1": 0, "Pemain 2": 0}
    players = ["Pemain 1", "Pemain 2"]
    winner = None

    while not winner:
        for player in players:
            positions[player] = move_player(player, positions[player])
            if positions[player] == 100:
                winner = player
                break

    print(f"\nSelamat {winner}! Kamu adalah pemenang Ular Tangga!")

if __name__ == "__main__":
    main()
