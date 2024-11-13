import os
import subprocess

# A list of available games and their executable paths
games = {
    "Game 1": r"C:\Games\Game1\game1.exe",  # Example path for Windows
    "Game 2": r"C:\Games\Game2\game2.exe",  # Example path for Windows
    "Game 3": r"/usr/games/game3",          # Example for Linux
}

def display_games():
    """Display a list of games for the user to choose from."""
    print("Available Games:")
    for idx, game in enumerate(games.keys(), 1):
        print(f"{idx}. {game}")

def launch_game(game_name):
    """Launch the selected game by its name."""
    game_path = games.get(game_name)
    if game_path and os.path.exists(game_path):
        try:
            print(f"Launching {game_name}...")
            subprocess.run(game_path, check=True)  # Launch the game
        except subprocess.CalledProcessError as e:
            print(f"Error while launching {game_name}: {e}")
    else:
        print(f"Game '{game_name}' is not available or path is invalid.")

def main():
    """Main function to handle the game launcher."""
    while True:
        display_games()
        try:
            choice = int(input("Enter the number of the game you want to launch (or 0 to exit): "))
            if choice == 0:
                print("Exiting the game launcher.")
                break
            elif 1 <= choice <= len(games):
                selected_game = list(games.keys())[choice - 1]
                launch_game(selected_game)
            else:
                print("Invalid choice, please try again.")
        except ValueError:
            print("Please enter a valid number.")

if __name__ == "__main__":
    main()

