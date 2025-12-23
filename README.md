import random
from datetime import datetime

HOOKS = [
    "Stop scrolling — this will change how you see {topic}.",
    "Most people do {topic} wrong. Here’s the right way:",
    "If you only learn ONE thing about {topic}, make it this:",
    "Here’s the uncomfortable truth about {topic}:",
    "This is the fastest way to improve {topic} today:"
]

CTAS = [
    "Save this post for later ✅",
    "Comment “DONE” and I’ll send you a checklist 📩",
    "Share this with a friend who needs it 🤝",
    "Follow for more daily tips 🔥",
    "Drop your question in comments 👇"
]

HASHTAG_BANK = {
    "fitness": ["#fitness", "#bodybuilding", "#workout", "#gym", "#nutrition", "#fatloss", "#musclebuilding"],
    "business": ["#business", "#marketing", "#entrepreneur", "#sales", "#branding", "#startup"],
    "content": ["#contentcreator", "#instagramgrowth", "#socialmediamarketing", "#reels", "#contentstrategy"],
    "general": ["#motivation", "#success", "#mindset", "#dailyhabits", "#selfimprovement"]
}

POST_TEMPLATES = [
    {
        "type": "Educational",
        "structure": [
            "1) {tip1}",
            "2) {tip2}",
            "3) {tip3}",
            "Bonus: {bonus}"
        ]
    },
    {
        "type": "Motivational",
        "structure": [
            "You don’t need motivation — you need a system.",
            "Do this daily: {tip1}",
            "Avoid this: {tip2}",
            "Remember: {bonus}"
        ]
    },
    {
        "type": "Nutrition",
        "structure": [
            "Quick rule: {tip1}",
            "Best choice: {tip2}",
            "Worst trap: {tip3}",
            "Simple plan: {bonus}"
        ]
    }
]

def generate_caption(topic, niche="general"):
    hook = random.choice(HOOKS).format(topic=topic)

    template = random.choice(POST_TEMPLATES)
    tips = {
        "tip1": f"Focus on one clear goal for {topic}.",
        "tip2": f"Track your progress (even a simple note works).",
        "tip3": f"Remove the biggest distraction around {topic}.",
        "bonus": f"Repeat this for 7 days and measure the difference."
    }

    body_lines = [line.format(**tips) for line in template["structure"]]
    cta = random.choice(CTAS)

    hashtags = HASHTAG_BANK.get(niche, HASHTAG_BANK["general"])
    hashtags = " ".join(random.sample(hashtags, min(6, len(hashtags))))

    caption = "\n".join([
        hook,
        "",
        f"Post type: {template['type']}",
        "",
        *body_lines,
        "",
        cta,
        "",
        hashtags
    ])

    return caption

def save_to_file(text, filename="generated_content.txt"):
    with open(filename, "a", encoding="utf-8") as f:
        f.write("\n" + "="*50 + "\n")
        f.write(datetime.now().strftime("%Y-%m-%d %H:%M:%S") + "\n\n")
        f.write(text + "\n")

if __name__ == "__main__":
    print("=== Content Generator (Instagram Ready) ===")
    topic = input("Enter your topic (e.g., fat loss, creatine, discipline): ").strip()
    niche = input("Enter niche (fitness/business/content/general): ").strip().lower()

    caption = generate_caption(topic, niche)
    print("\n--- GENERATED CAPTION ---\n")
    print(caption)

    save = input("\nSave to file? (y/n): ").strip().lower()
    if save == "y":
        save_to_file(caption)
        print("Saved ✅ (generated_content.txt)")

