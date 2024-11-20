# project-akhir
project terakhir
import time
from datetime import datetime

class Obat:
    def __init__(self, nama_obat, waktu_minum):
        """
        Inisialisasi Obat
        :param nama_obat: Nama obat
        :param waktu_minum: Waktu minum obat (format: HH:MM)
        """
        self.nama_obat = nama_obat
        self.waktu_minum = waktu_minum

    def __str__(self):
        return f"{self.nama_obat} - {self.waktu_minum}"


class PengingatObat:
    def __init__(self):
        """
        Inisialisasi Pengingat Obat dengan daftar kosong
        """
        self.daftar_obat = []

    def tambah_obat(self, nama_obat, waktu_minum):
        """
        Tambahkan obat ke daftar pengingat
        """
        self.daftar_obat.append(Obat(nama_obat, waktu_minum))
        print(f"Obat '{nama_obat}' pada waktu {waktu_minum} berhasil ditambahkan!")

    def hapus_obat(self, nama_obat):
        """
        Hapus obat dari daftar pengingat
        """
        for obat in self.daftar_obat:
            if obat.nama_obat == nama_obat:
                self.daftar_obat.remove(obat)
                print(f"Obat '{nama_obat}' berhasil dihapus!")
                return
        print(f"Obat '{nama_obat}' tidak ditemukan.")

    def tampilkan_daftar(self):
        """
        Tampilkan semua daftar obat
        """
        if not self.daftar_obat:
            print("Daftar obat kosong.")
        else:
            print("Daftar Obat:")
            for obat in self.daftar_obat:
                print(f"- {obat}")

    def cek_pengingat(self):
        """
        Periksa apakah ada obat yang harus diminum saat ini
        """
        sekarang = datetime.now().strftime("%H:%M")
        for obat in self.daftar_obat:
            if obat.waktu_minum == sekarang:
                print(f"Waktunya minum obat: {obat.nama_obat} ({obat.waktu_minum})")

    def mulai_pengingat(self):
        """
        Mulai pengingat dengan pengecekan waktu secara berkala
        """
        print("Pengingat berjalan... Tekan CTRL+C untuk berhenti.")
        try:
            while True:
                self.cek_pengingat()
                time.sleep(60)  # Periksa setiap menit
        except KeyboardInterrupt:
            print("\nPengingat dihentikan.")


# Contoh Penggunaan
if __name__ == "__main__":
    pengingat = PengingatObat()
    pengingat.tambah_obat("Paracetamol", "08:00")
    pengingat.tambah_obat("Vitamin C", "14:00")
    pengingat.tambah_obat("Aspirin", "20:00")
    
    pengingat.tampilkan_daftar()
    
    # Aktifkan pengingat (akan berjalan terus hingga dihentikan)
    pengingat.mulai_pengingat()
