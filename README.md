import streamlit as st
import pandas as pd

st.title("🚀 Spark SaaS Forecast Engine")

lending_amount = st.number_input("ยอด Lending (USD):", 100, 100000, step=100)

base_airdrop_rate = 0.5
invite_multiplier = 0.1
invite_range = [0, 1, 5, 10, 20, 50, 100]
result = []
for invite in invite_range:
    reward = lending_amount * (base_airdrop_rate + invite * invite_multiplier)
    result.append({"Invite": invite, "Airdrop ($)": reward})
df = pd.DataFrame(result)

st.subheader("📊 Forecast Table")
st.table(df)

st.subheader("📈 Forecast Chart")
st.line_chart(df.set_index("Invite"))

st.download_button("📥 Download CSV", df.to_csv().encode('utf-8'), "spark_forecast.csv", "text/csv")
