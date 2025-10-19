# Chatbot.py
Customer service 
# Chatbot Customer Service Sederhana
# Dibuat untuk dijalankan di Anaconda (Python environment)
# Tema: Menjawab pertanyaan umum pelanggan, memberikan info produk, menangani pesanan sederhana.

# Simulasi data produk (bisa diperluas)
produk = {
    "laptop": {"harga": 5000000, "stok": 10, "pengiriman": "Gratis ongkir untuk wilayah Jabodetabek"},
    "smartphone": {"harga": 3000000, "stok": 5, "pengiriman": "Ongkir Rp 50.000 untuk luar Jabodetabek"},
    "headphone": {"harga": 500000, "stok": 20, "pengiriman": "Gratis ongkir untuk semua wilayah"}
}

# Simulasi data pesanan (untuk demo, gunakan ID pesanan fiktif)
pesanan = {
    "ORD001": {"status": "Sedang diproses", "produk": "laptop"},
    "ORD002": {"status": "Dikirim", "produk": "smartphone"}
}

def chatbot():
    print("Selamat datang di Customer Service Bot!")
    print("Ketik 'keluar' untuk mengakhiri percakapan.")
    print("-" * 50)
    
    while True:
        user_input = input("Anda: ").lower().strip()
        
        if user_input == "keluar":
            print("Bot: Terima kasih telah menggunakan layanan kami. Sampai jumpa!")
            break
        
        # Jawab pertanyaan umum
        if "halo" in user_input or "hai" in user_input:
            print("Bot: Halo! Ada yang bisa saya bantu?")
        
        elif "produk" in user_input and "harga" in user_input:
            produk_nama = input("Bot: Produk apa yang ingin Anda tanyakan harganya? ").lower()
            if produk_nama in produk:
                print(f"Bot: Harga {produk_nama} adalah Rp {produk[produk_nama]['harga']:,}.")
            else:
                print("Bot: Maaf, produk tersebut tidak ditemukan.")
        
        elif "produk" in user_input and "stok" in user_input:
            produk_nama = input("Bot: Produk apa yang ingin Anda tanyakan stoknya? ").lower()
            if produk_nama in produk:
                print(f"Bot: Stok {produk_nama} tersedia {produk[produk_nama]['stok']} unit.")
            else:
                print("Bot: Maaf, produk tersebut tidak ditemukan.")
        
        elif "pengiriman" in user_input:
            produk_nama = input("Bot: Produk apa yang ingin Anda tanyakan pengirimannya? ").lower()
            if produk_nama in produk:
                print(f"Bot: {produk[produk_nama]['pengiriman']}.")
            else:
                print("Bot: Maaf, produk tersebut tidak ditemukan.")
        
        elif "pesan produk" in user_input:
            produk_nama = input("Bot: Produk apa yang ingin Anda pesan? ").lower()
            if produk_nama in produk and produk[produk_nama]['stok'] > 0:
                jumlah = int(input("Bot: Berapa jumlah yang ingin dipesan? "))
                if jumlah <= produk[produk_nama]['stok']:
                    total = jumlah * produk[produk_nama]['harga']
                    print(f"Bot: Pesanan Anda untuk {jumlah} {produk_nama} telah dikonfirmasi. Total: Rp {total:,}.")
                    produk[produk_nama]['stok'] -= jumlah  # Kurangi stok
                    # Simulasi ID pesanan baru
                    id_pesanan = f"ORD{len(pesanan)+1:03d}"
                    pesanan[id_pesanan] = {"status": "Sedang diproses", "produk": produk_nama}
                    print(f"Bot: ID Pesanan Anda: {id_pesanan}. Simpan ID ini untuk cek status.")
                else:
                    print("Bot: Maaf, stok tidak mencukupi.")
            else:
                print("Bot: Maaf, produk tidak tersedia atau stok habis.")
        
        elif "cek status pesanan" in user_input:
            id_pesanan = input("Bot: Masukkan ID Pesanan Anda: ").upper()
            if id_pesanan in pesanan:
                status = pesanan[id_pesanan]['status']
                produk_pesanan = pesanan[id_pesanan]['produk']
                print(f"Bot: Status pesanan {id_pesanan} ({produk_pesanan}): {status}.")
            else:
                print("Bot: Maaf, ID pesanan tidak ditemukan.")
        
        else:
            print("Bot: Maaf, saya tidak mengerti. Coba tanyakan tentang produk, harga, stok, pengiriman, pesan produk, atau cek status pesanan.")
        
        print("-" * 50)

# Jalankan chatbot
if __name__ == "__main__":
    chatbot()
