import json

# Database to map keywords to visual elements (shapes, colors, lines)
visual_mapping = {
    "sky": {"shape": "circle", "color": "blue", "line": "wavy"},
    "water": {"shape": "wave", "color": "aqua", "line": "curvy"},
    "fire": {"shape": "triangle", "color": "red", "line": "jagged"},
    "tree": {"shape": "rectangle", "color": "green", "line": "straight"},
    "cloud": {"shape": "oval", "color": "white", "line": "soft"},
    "night": {"shape": "star", "color": "dark blue", "line": "dotted"},
    # Add more keywords as needed
}

# Function to process a dream and translate it into visual elements
def translate_dream(dream):
    dream_keywords = dream.lower().split()  # Split dream into words
    translation = []

    for word in dream_keywords:
        if word in visual_mapping:
            translation.append({"keyword": word, **visual_mapping[word]})

    return translation

# Save translations to a JSON file
def save_translation(dream, translation):
    data = {
        "dream": dream,
        "translation": translation
    }
    
    with open("dream_translations.json", "a") as file:
        file.write(json.dumps(data) + "\n")

# Main program loop
def main():
    print("Dream Translation Tool")
    print("Enter a dream description, and I will translate it into shapes, colors, and lines.")

    while True:
        dream = input("Enter your dream (or type 'exit' to quit): ")
        if dream.lower() == "exit":
            print("Goodbye!")
            break

        translation = translate_dream(dream)

        if translation:
            print("\nTranslation:")
            for item in translation:
                print(f"Keyword: {item['keyword']}, Shape: {item['shape']}, Color: {item['color']}, Line: {item['line']}")

            save_translation(dream, translation)
            print("\nTranslation saved!\n")
        else:
            print("No keywords recognized in the dream. Try again.\n")

if __name__ == "__main__":
    main()

