# Praktikum 1

## Import Library 

    import numpy as np
    import matplotlib.pyplot as plt
​
# Definisikan fungsi yang dicari nilai akarnya  

    def f(x):
        return x**3 - x - 2  # Contoh fungsi: bisa diganti
​
#Fungsi metode regula falsi 

    def regula_falsi(a, b, tol=1e-5, max_iter=100):
        if f(a) * f(b) >= 0:
            print("f(a) dan f(b) harus memiliki tanda yang berbeda.")
            return None
    
        iterasi = 0
        data_iterasi = []
    
        print("Iterasi\t a\t\t b\t\t c\t\t f(c)\t\t Error")
        while iterasi < max_iter:
            c = b - f(b)*(b - a)/(f(b) - f(a))
            fc = f(c)
            error = abs(f(c))
    
            data_iterasi.append((iterasi, a, b, c, fc, error))
            print(f"{iterasi}\t {a:.6f}\t {b:.6f}\t {c:.6f}\t {fc:.6f}\t {error:.6f}")
    
            if error < tol:
                break
    
            if f(a)*fc < 0:
                b = c
            else:
                a = c
    
            iterasi += 1
    
        return c, data_iterasi`​
# input batas awal iterasi 

    a = 1  
    b = 2  
​
# Jalankan regula falsi

    akar, data = regula_falsi(a, b)
    print(f"\nAkar ditemukan: {akar:.6f}")
​
# Buat grafik fungsi dan proses iterasi 

    x_vals = np.linspace(a-1, b+1, 400)
    y_vals = f(x_vals)

    plt.figure(figsize=(10, 6))
    plt.plot(x_vals, y_vals, label="f(x)", color='blue')
    plt.axhline(0, color='black', linestyle='--')
    plt.title("Metode Regula Falsi - Proses Iterasi")
    plt.xlabel("x")
    plt.ylabel("f(x)")
    
    plt.grid(True)
    plt.legend()
    plt.show()

​
# Menambahkan titik hasil akar aprokmasi 

    c_last, fc_last = data[-1][3], data[-1][4]  
    plt.plot(c_last, fc_last, 'ro', label='Akar Hampiran')
    plt.annotate(f'Akar ≈ {c_last:.6f}', (c_last, fc_last),
                 textcoords="offset points", xytext=(0, 10), ha='center', fontsize=9, color='red')
    ​
    plt.grid(True)
    plt.legend()
    plt.show()
