
# Fungsi untuk mengubah angka menjadi format Rupiah
def rupiah(nilai):
    return "Rp{:,.0f}".format(nilai).replace(",", ".")


# 1. SUPERCLASS: Karyawan
class Karyawan:
    def __init__(self, nama, id_karyawan, gaji_pokok):
        self.nama = nama
        self.id_karyawan = id_karyawan
        self.__gaji_pokok = 0
        self.gaji_pokok = gaji_pokok

    # Getter untuk mengambil gaji pokok
    @property
    def gaji_pokok(self):
        return self.__gaji_pokok

    # Setter untuk mengubah gaji pokok
    @gaji_pokok.setter
    def gaji_pokok(self, nilai):
        if nilai <= 0:
            print("Gaji pokok harus lebih dari 0!")
        else:
            self.__gaji_pokok = nilai
            print("Gaji pokok berhasil diubah.")

    # Menghitung gaji dasar
    def hitung_gaji_total(self):
        return self.__gaji_pokok

    # Menampilkan informasi dasar karyawan
    def tampilkan_info(self):
        print("Nama         :", self.nama)
        print("ID Karyawan  :", self.id_karyawan)
        print("Gaji Pokok   :", rupiah(self.gaji_pokok))


# 2. SUBCLASS: KaryawanTetap
class KaryawanTetap(Karyawan):
    def __init__(self, nama, id_karyawan, gaji_pokok, tunjangan):
        super().__init__(nama, id_karyawan, gaji_pokok)
        self.tunjangan = tunjangan

    # Overriding method hitung_gaji_total()
    def hitung_gaji_total(self):
        return self.gaji_pokok + self.tunjangan

    # Overriding method tampilkan_info()
    def tampilkan_info(self):
        print("\n=== KARYAWAN TETAP ===")
        print("Nama         :", self.nama)
        print("ID Karyawan  :", self.id_karyawan)
        print("Gaji Pokok   :", rupiah(self.gaji_pokok))
        print("Tunjangan    :", rupiah(self.tunjangan))
        print("Total Gaji   :", rupiah(self.hitung_gaji_total()))


# 3. SUBCLASS: KaryawanKontrak
class KaryawanKontrak(Karyawan):
    def __init__(self, nama, id_karyawan, gaji_pokok,
                 jam_lembur, tarif_lembur):
        super().__init__(nama, id_karyawan, gaji_pokok)
        self.jam_lembur = jam_lembur
        self.tarif_lembur = tarif_lembur

    # Overriding method hitung_gaji_total()
    def hitung_gaji_total(self):
        return self.gaji_pokok + (
            self.jam_lembur * self.tarif_lembur
        )

    # Overriding method tampilkan_info()
    def tampilkan_info(self):
        total_lembur = self.jam_lembur * self.tarif_lembur

        print("\n=== KARYAWAN KONTRAK ===")
        print("Nama         :", self.nama)
        print("ID Karyawan  :", self.id_karyawan)
        print("Gaji Pokok   :", rupiah(self.gaji_pokok))
        print("Jam Lembur   :", self.jam_lembur, "jam")
        print("Tarif Lembur :", rupiah(self.tarif_lembur), "/jam")
        print("Total Lembur :", rupiah(total_lembur))
        print("Total Gaji   :", rupiah(self.hitung_gaji_total()))


# 4. MAIN PROGRAM
if __name__ == "__main__":

    # Membuat objek karyawan tetap
    karyawan1 = KaryawanTetap(
        "Nurul Hikma Awalia",
        "20892",
        4500000,
        850000
    )

    # Membuat objek karyawan kontrak
    karyawan2 = KaryawanKontrak(
        "Widya Dwi Puspita",
        "52912",
        3500000,
        15,
        40000
    )

    # Menyimpan objek ke dalam list
    daftar_karyawan = [karyawan1, karyawan2]

    # Demonstrasi polymorphism
    print("===== SISTEM PENGGAJIAN KARYAWAN =====")

    for karyawan in daftar_karyawan:
        karyawan.tampilkan_info()
        print("-" * 40)

    # Demonstrasi encapsulation
    print("\n===== PENGUJIAN ENCAPSULATION =====")

    print(
        "Gaji sebelum diubah:",
        rupiah(karyawan1.gaji_pokok)
    )

    # Menguji nilai gaji tidak valid
    print("\nMengubah gaji dengan nilai tidak valid:")
    karyawan1.gaji_pokok = -500000

    # Menguji nilai gaji valid
    print("\nMengubah gaji dengan nilai valid:")
    karyawan1.gaji_pokok = 5200000

    # Menampilkan informasi setelah perubahan
    print("\nInformasi setelah perubahan:")
    karyawan1.tampilkan_info()

