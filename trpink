import streamlit as st

st.set_page_config(
    page_title="Taschenrechner",
    page_icon="🩷",
    layout="centered"
)

# -----------------------------
# DESIGN
# -----------------------------

st.markdown("""
<style>

.stApp {
    background: linear-gradient(135deg, #fff5f8, #ffe4ef);
}

.main {
    max-width: 500px;
}

.calculator {
    background: white;
    padding: 30px;
    border-radius: 30px;
    box-shadow: 0 10px 35px rgba(255, 105, 150, 0.15);
}

.title {
    text-align: center;
    color: #f45b91;
    font-size: 36px;
    font-weight: bold;
    margin-bottom: 25px;
}

.display {
    background: #fff7fa;
    border: 2px solid #ffd5e3;
    border-radius: 20px;
    padding: 25px;
    text-align: right;
    font-size: 42px;
    font-weight: bold;
    color: #333;
    margin-bottom: 20px;
}

.stButton > button {
    width: 100%;
    height: 65px;
    border-radius: 18px;
    border: none;
    background-color: #fff1f6;
    color: #444;
    font-size: 24px;
    font-weight: 600;
    box-shadow: 0 4px 10px rgba(255, 100, 150, 0.12);
    transition: 0.2s;
}

.stButton > button:hover {
    background-color: #ffd9e7;
    color: #ed4f88;
    transform: scale(1.03);
}

.footer {
    text-align: center;
    color: #f28aae;
    margin-top: 25px;
    font-size: 16px;
}

</style>
""", unsafe_allow_html=True)


# -----------------------------
# SESSION STATE
# -----------------------------

if "display" not in st.session_state:
    st.session_state.display = "0"

if "erste_zahl" not in st.session_state:
    st.session_state.erste_zahl = None

if "operator" not in st.session_state:
    st.session_state.operator = None


# -----------------------------
# FUNKTION
# -----------------------------

def druecke_taste(taste):

    # Zahlen
    if taste in "0123456789":

        if st.session_state.display == "0":
            st.session_state.display = taste
        else:
            st.session_state.display += taste

    # Komma
    elif taste == ",":
        if "," not in st.session_state.display:
            st.session_state.display += ","

    # Löschen
    elif taste == "C":
        st.session_state.display = "0"
        st.session_state.erste_zahl = None
        st.session_state.operator = None

    # Vorzeichen
    elif taste == "±":

        if st.session_state.display != "0":

            if st.session_state.display.startswith("-"):
                st.session_state.display = \
                    st.session_state.display[1:]
            else:
                st.session_state.display = \
                    "-" + st.session_state.display

    # Operator
    elif taste in ["+", "−", "×", "÷"]:

        st.session_state.erste_zahl = float(
            st.session_state.display.replace(",", ".")
        )

        st.session_state.operator = taste
        st.session_state.display = "0"

    # Gleich
    elif taste == "=":

        if (
            st.session_state.erste_zahl is not None
            and st.session_state.operator is not None
        ):

            zweite_zahl = float(
                st.session_state.display.replace(",", ".")
            )

            erste_zahl = st.session_state.erste_zahl
            operator = st.session_state.operator

            if operator == "+":
                ergebnis = erste_zahl + zweite_zahl

            elif operator == "−":
                ergebnis = erste_zahl - zweite_zahl

            elif operator == "×":
                ergebnis = erste_zahl * zweite_zahl

            elif operator == "÷":

                if zweite_zahl == 0:
                    st.session_state.display = "Fehler 🩷"
                    return

                ergebnis = erste_zahl / zweite_zahl

            # Schön formatieren
            if ergebnis == int(ergebnis):
                st.session_state.display = str(int(ergebnis))
            else:
                st.session_state.display = str(
                    round(ergebnis, 10)
                )

            st.session_state.erste_zahl = None
            st.session_state.operator = None


# -----------------------------
# TASCHENRECHNER
# -----------------------------

st.markdown('<div class="calculator">', unsafe_allow_html=True)

st.markdown(
    '<div class="title">🩷 Taschenrechner</div>',
    unsafe_allow_html=True
)

# Display
st.markdown(
    f'<div class="display">{st.session_state.display}</div>',
    unsafe_allow_html=True
)


# -----------------------------
# TASTEN
# -----------------------------

zeilen = [
    ["C", "±", "÷", "×"],
    ["7", "8", "9", "−"],
    ["4", "5", "6", "+"],
    ["1", "2", "3", "="],
    ["0", ",", "", ""]
]


for zeile_nummer, zeile in enumerate(zeilen):

    spalten = st.columns(4)

    for i, taste in enumerate(zeile):

        with spalten[i]:

            if taste != "":

                if st.button(
                    taste,
                    key=f"taste_{zeile_nummer}_{i}",
                    use_container_width=True
                ):

                    druecke_taste(taste)
                    st.rerun()


st.markdown(
    '<div class="footer">♡ Mit Liebe gerechnet ✨</div>',
    unsafe_allow_html=True
)

st.markdown("</div>", unsafe_allow_html=True)
