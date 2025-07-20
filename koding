import streamlit as st

# Konfigurasi halaman
st.set_page_config(page_title="Kalkulator Gas Ideal", page_icon="🧪")

# Judul dan deskripsi
st.title("🧪 Kalkulator Hukum Gas Ideal")
st.write("Gunakan persamaan PV = nRT untuk menghitung salah satu variabel.")

st.latex("PV = nRT")
st.markdown("Dengan R = 0.0821 L·atm/mol·K")

R = 0.0821  # Konstanta gas dalam L·atm/mol·K

# Input variabel sebagai teks (agar bisa dikosongkan)
P_input = st.text_input("Tekanan (P) dalam atm (kosongkan jika ingin dihitung)")
V_input = st.text_input("Volume (V) dalam liter (kosongkan jika ingin dihitung)")
n_input = st.text_input("Jumlah mol (n) (kosongkan jika ingin dihitung)")
T_input = st.text_input("Suhu (T) dalam Kelvin (kosongkan jika ingin dihitung)")

# Fungsi untuk mengonversi input ke float
def to_float(value):
    try:
        return float(value) if value else None
    except ValueError:
        return None

# Konversi
P = to_float(P_input)
V = to_float(V_input)
n = to_float(n_input)
T = to_float(T_input)

# Deteksi variabel kosong
inputs = {'P': P, 'V': V, 'n': n, 'T': T}
empty_vars = [var for var, value in inputs.items() if value is None]

# Tombol untuk menghitung
if st.button("Hitung"):
    # Validasi input: tidak boleh ada nilai <= 0 selain variabel yang dihitung
    invalid_values = [var for var, value in inputs.items() if value is not None and value <= 0]
    
    if invalid_values:
        st.error(f"Nilai {', '.join(invalid_values)} harus lebih besar dari 0.")
    elif len(empty_vars) != 1:
        st.error("Tolong kosongkan tepat satu variabel yang ingin dihitung.")
    else:
        try:
            if P is None:
                P = (n * R * T) / V
                st.success(f"Tekanan (P) = {P:.4f} atm")
            elif V is None:
                V = (n * R * T) / P
                st.success(f"Volume (V) = {V:.4f} liter")
            elif n is None:
                n = (P * V) / (R * T)
                st.success(f"Jumlah mol (n) = {n:.4f} mol")
            elif T is None:
                T = (P * V) / (n * R)
                st.success(f"Suhu (T) = {T:.2f} K")
        except Exception as e:
            st.error(f"Terjadi kesalahan dalam perhitungan: {e}")
