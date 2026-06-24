import streamlit as st
import random

st.set_page_config(
    page_title="Choice Theory Adventure",
    page_icon="🌟",
    layout="centered"
)

# -----------------------------
# Question Bank
# -----------------------------
QUESTIONS = [
    {
        "question": "Your friend won't let you play their game. What is the best choice?",
        "options": [
            "Yell at them",
            "Ask calmly if you can join later",
            "Push them",
            "Take the game away"
        ],
        "answer": "Ask calmly if you can join later",
        "explanation": "Choice Theory teaches that we can choose helpful actions instead of reacting with anger."
    },
    {
        "question": "You feel angry because someone laughed at your drawing. What can you control?",
        "options": [
            "Their thoughts",
            "Their feelings",
            "Your response",
            "The past"
        ],
        "answer": "Your response",
        "explanation": "Reality Therapy reminds us that we can control our own choices and actions."
    },
    {
        "question": "You forgot your homework. What is the most responsible choice?",
        "options": [
            "Blame a friend",
            "Lie to the teacher",
            "Tell the truth and make a plan",
            "Hide from the teacher"
        ],
        "answer": "Tell the truth and make a plan",
        "explanation": "Taking responsibility helps us solve problems and build trust."
    },
    {
        "question": "You are feeling upset. Which action may help?",
        "options": [
            "Take deep breaths",
            "Break something",
            "Yell loudly",
            "Refuse to talk forever"
        ],
        "answer": "Take deep breaths",
        "explanation": "Deep breathing can help calm our emotions so we can make better choices."
    },
    {
        "question": "Your friend wants a different game than you. What is a good choice?",
        "options": [
            "Argue until they agree",
            "Take turns choosing",
            "Quit being friends",
            "Call them names"
        ],
        "answer": "Take turns choosing",
        "explanation": "Good relationships are important in Choice Theory."
    },
    {
        "question": "Which need is about having friends and feeling connected?",
        "options": [
            "Belonging",
            "Power",
            "Freedom",
            "Fun"
        ],
        "answer": "Belonging",
        "explanation": "Belonging means feeling cared for, accepted, and connected to others."
    },
    {
        "question": "You are frustrated with a difficult task. What is a helpful choice?",
        "options": [
            "Give up immediately",
            "Ask for help",
            "Throw your work away",
            "Get angry at everyone"
        ],
        "answer": "Ask for help",
        "explanation": "Asking for help is a strong and responsible choice."
    },
    {
        "question": "Which statement matches Choice Theory?",
        "options": [
            "Other people control my feelings",
            "I can choose how I respond",
            "I can control everyone",
            "Problems solve themselves"
        ],
        "answer": "I can choose how I respond",
        "explanation": "Choice Theory teaches that our choices matter."
    }
]

TOTAL_QUESTIONS = 5

# -----------------------------
# Session State
# -----------------------------
if "game_started" not in st.session_state:
    st.session_state.game_started = False

if "score" not in st.session_state:
    st.session_state.score = 0

if "current_question" not in st.session_state:
    st.session_state.current_question = 0

if "question_set" not in st.session_state:
    st.session_state.question_set = []

if "answered" not in st.session_state:
    st.session_state.answered = False

if "selected_answer" not in st.session_state:
    st.session_state.selected_answer = None


# -----------------------------
# Functions
# -----------------------------
def start_game():
    st.session_state.game_started = True
    st.session_state.score = 0
    st.session_state.current_question = 0
    st.session_state.question_set = random.sample(
        QUESTIONS,
        TOTAL_QUESTIONS
    )
    st.session_state.answered = False
    st.session_state.selected_answer = None


def next_question():
    st.session_state.current_question += 1
    st.session_state.answered = False
    st.session_state.selected_answer = None


# -----------------------------
# Title Screen
# -----------------------------
st.title("🌟 Choice Theory Adventure")
st.subheader("Learn how to make helpful choices!")

st.write(
    """
    🎮 Answer questions about feelings, friendships, and good choices.

    ⭐ Earn points for correct answers!

    🏆 Can you become a Choice Theory Champion?
    """
)

# -----------------------------
# Start Button
# -----------------------------
if not st.session_state.game_started:
    if st.button("🚀 Start Adventure"):
        start_game()
        st.rerun()

# -----------------------------
# Game Screen
# -----------------------------
if st.session_state.game_started:

    if st.session_state.current_question < TOTAL_QUESTIONS:

        q = st.session_state.question_set[
            st.session_state.current_question
        ]

        progress = (
            st.session_state.current_question
        ) / TOTAL_QUESTIONS

        st.progress(progress)

        st.write(
            f"### Question {st.session_state.current_question + 1} of {TOTAL_QUESTIONS}"
        )

        st.info(q["question"])

        choice = st.radio(
            "Choose your answer:",
            q["options"],
            key=f"radio_{st.session_state.current_question}"
        )

        if not st.session_state.answered:

            if st.button("Submit Answer"):

                st.session_state.selected_answer = choice
                st.session_state.answered = True

                if choice == q["answer"]:
                    st.session_state.score += 1

                st.rerun()

        else:

            if st.session_state.selected_answer == q["answer"]:
                st.success("✅ Correct!")

            else:
                st.error("❌ Not quite!")

            st.write(
                f"**Explanation:** {q['explanation']}"
            )

            st.write(
                f"**Correct Answer:** {q['answer']}"
            )

            if st.button("➡️ Next Question"):
                next_question()
                st.rerun()

    # -----------------------------
    # Results Screen
    # -----------------------------
    else:

        st.header("🏆 Adventure Complete!")

        score = st.session_state.score

        st.metric(
            "Final Score",
            f"{score}/{TOTAL_QUESTIONS}"
        )

        percentage = (score / TOTAL_QUESTIONS) * 100

        if percentage >= 80:
            st.balloons()
            st.success(
                "Amazing! You are a Choice Theory Champion! 🌟"
            )

        elif percentage >= 60:
            st.success(
                "Great job! You made many helpful choices! 😊"
            )

        else:
            st.info(
                "Keep practicing! Every day is a new chance to make good choices. 💪"
            )

        st.write("### What We Learned")

        st.markdown("""
        - We can choose how we respond.
        - We cannot control other people.
        - Good relationships are important.
        - Taking responsibility helps solve problems.
        - Calm choices help us manage emotions.
        """)

        if st.button("🔄 Play Again"):
            start_game()
            st.rerun()
