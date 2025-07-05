# Week-1-Assignment
import streamlit as st

st.set_page_config(page_title="Quiz App")
st.title("🎓 Welcome to Quiz App")

# Quiz data: questions, options, and correct answers
questions = [
    {
        "question": "Q1: Who was the first Prime Minister of independent India?",
        "options": ["Sardar Vallabhbhai Patel", "Jawaharlal Nehru", "Mahatma Gandhi", "Dr. B.R. Ambedkar"],
        "answer": "Jawaharlal Nehru"
    },
    {
        "question": "Q2: Which Indian film won the Academy Award (Oscar) for Best Original Song in 2023?",
        "options": ["Lagaan", "Slumdog Millionaire", "RRR", "Dangal"],
        "answer": "RRR"
    },
    {
        "question": "Q3: Which article of the Indian Constitution gives special status to Jammu and Kashmir (now revoked)?",
        "options": ["Article 356", "Article 370", "Article 377", "Article 21"],
        "answer": "Article 370"
    },
    {
        "question": "Q4: Who is the current Prime Minister of India (as of 2025)?",
        "options": ["Rahul Gandhi", "Narendra Modi", "Arvind Kejriwal", "Amit Shah"],
        "answer": "Narendra Modi"
    },
    {
        "question": "Q5: In which year did India gain independence from British rule?",
        "options": ["1945", "1946", "1947", "1950"],
        "answer": "1947"
    }
]

user_answers = []
score = 0

with st.form("quiz_form"):
    st.subheader("Please answer all the questions below:")

    for i, q in enumerate(questions):
        options_with_placeholder = ["-- Select an option --"] + q["options"]
        user_choice = st.selectbox(q["question"], options_with_placeholder, key=f"q{i}")
        user_answers.append(user_choice)

    # ✅ Submit button must be inside the form
    submitted = st.form_submit_button("Submit Quiz")

# ✅ Process submission and result outside the form
if 'submitted' in locals() and submitted:
    if "-- Select an option --" in user_answers:
        st.warning("⚠️ Please answer all the questions before submitting.")
    else:
        for i in range(len(questions)):
            if user_answers[i] == questions[i]["answer"]:
                score += 1

        st.write("### Your Score:", score, "/ 5")

        if score >= 4:
            st.success("🎉 Congratulations! You passed the quiz!")
        else:
            st.error("❌ You did not pass the quiz. Please try again.")
