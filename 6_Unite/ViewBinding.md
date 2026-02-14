🌸 Resim Değiştirme Uygulaması (View Binding Örneği)
View Binding yapısı, ArrayList kullanımı ve Nesne Yönelimli Programlama (OOP) konularını kapsar.

🏗️ 1. Adım: View Binding Aktif Etme
Android Studio'da arayüz elemanlarına (buton, metin vb.) en güvenli ve hızlı şekilde ulaşmak için build.gradle (Module :app) dosyasında bu özelliği açmamız gerekir:

build.gradle (Module :app)
android {
    // ... diğer ayarlar
    buildFeatures {
        viewBinding = true
    }
}
Not: Bu işlemden sonra sağ üstteki "Sync Now" butonuna basmayı unutmayın.

Projeye 2 Buton, 1 Textview, 1 tane de ImageView ekleyiniz.

📦 2. Adım: Veri Modeli (cicek.java)
Her bir çiçeğin bilgisini, resmini ve sıra numarasını bir arada tutmak için bir sınıf oluşturuyoruz.

public class cicek {
    String bilgi; // Çiçeğin ismi
    int gorsel;   // Resmin ID'si (R.drawable.resim_adi)
    int siraNo;   // Sıralama numarası

    // Yapıcı Metot (Constructor)
    public cicek(String bilgi, int gorsel, int siraNo) {
        this.bilgi = bilgi;
        this.gorsel = gorsel;
        this.siraNo = siraNo;
    }
}
🚀 3. Adım: Uygulama Mantığı (MainActivity.java)
Burada listemizi oluşturuyor ve butonlara basıldığında resmin değişmesini sağlıyoruz.

Java
package com.example.resimDegistir;

import android.os.Bundle;
import android.view.View;
import androidx.appcompat.app.AppCompatActivity;
import com.example.myapplication.databinding.ActivityMainBinding;
import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
    private ActivityMainBinding binding;  // View Binding tanımlaması
    ArrayList<cicek> cicekArrayList;
    int seciliSiraNo;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // View Binding'i başlatma
        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());

        // Veri listesini hazırlama
        cicekArrayList = new ArrayList<>();
        cicek manolya = new cicek("Manolya", R.drawable.manolya, 1);
        cicek lale = new cicek("Lale", R.drawable.lale, 2);
        
        cicekArrayList.add(manolya);
        cicekArrayList.add(lale);

        // Uygulama açıldığında ilk çiçeği göster
        ekranGuncelle();
        seciliSiraNo = 0;
    }

    // İLERİ Butonuna basıldığında çalışır. (onClick özelliğinde ismi güncellemeyi unutmayın)
    public void ileriGitme(View view) {
        if (seciliSiraNo < cicekArrayList.size() - 1) {
            seciliSiraNo++;
           binding.imageViewGorsel.setImageResource(cicekArrayList.get(seciliSiraNo).gorsel);
           binding.textViewBilgi.setText("Bilgi: " + cicekArrayList.get(seciliSiraNo).bilgi);
        }
    }

    // GERİ Butonuna basıldığında çalışır
    public void geriGitme(View view) {
        if (seciliSiraNo > 0) {
            seciliSiraNo--;
            binding.imageViewGorsel.setImageResource(cicekArrayList.get(seciliSiraNo).gorsel);
            binding.textViewBilgi.setText("Bilgi: " + cicekArrayList.get(seciliSiraNo).bilgi);
        }
    }
}