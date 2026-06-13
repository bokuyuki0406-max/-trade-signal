import streamlit as st
import yfinance as yf

st.set_page_config(page_title="地合い判定", layout="centered")

st.title("🔥 EMAスイング・地合い判定")
st.write("今の相場がエントリーに適しているか判定します")

# データの取得
def get_status():
    vix = yf.Ticker("^VIX").history(period="1d")['Close'].iloc[-1]
    nk = yf.Ticker("^N225").history(period="2d")['Close']
    return vix, nk

try:
    vix, nk = get_status()
    nk_change = nk.iloc[-1] - nk.iloc[-2]

    # 判定ロジック
    st.header("今日の判定")
    if vix > 22:
        st.error(f"🔴 STOP：地合い最悪 (VIX: {vix:.2f})")
        st.subheader("無理は禁物！今は現金比率を高める時です。")
    elif nk_change < 0:
        st.warning(f"🟡 CAUTION：慎重に (日経前日比: {nk_change:.0f}円)")
        st.subheader("全体が下げています。強い個別銘柄だけに絞りましょう。")
    else:
        st.success(f"🟢 GO：地合い良好！ (VIX: {vix:.2f})")
        st.subheader("EMAの反転形が出たら積極的に狙っていきましょう。")

    st.write("---")
    st.write(f"・VIX指数（恐怖指数）: {vix:.2f}")
    st.write(f"・日経平均終値: {nk.iloc[-1]:.0f}円")

except:
    st.write("データ取得中... または市場が閉まっています。")

st.caption("※データはYahoo Financeから自動取得しています。")
