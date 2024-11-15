# Konsep Dasar Optimasi Gambar Next.Js

## Apa itu Optimasi Gambar?

Optimasi gambar adalah proses mengurangi ukuran file gambar tanpa menurunkan kualitas visualnya. Tujuan utamanya adalah membuat gambar lebih cepat dimuat di aplikasi web dan seluler, sehingga meningkatkan pengalaman pengguna. Beberapa teknik optimasi yang umum digunakan meliputi:

- **Image Compression** : Mengompres ukuran file gambar tanpa menurunkan kualitas visual.
- **Image Resizing** : Menyesuaikan dimensi gambar agar sesuai tampilan aplikasi, sehingga mencegah penggunaan gambar yang terlalu besar.
- **Image Format Selection** : Memilih format gambar yang paling efisien, seperti **WebP** atau **AVIF** yang biasanya lebih ringan dibandingkan JPEG atau PNG.
- **Lazy Loading** : Memuat gambar hanya saat pengguna hampir melihatnya, untuk menghemat data dan mempercepat pemuatan halaman.
- **Content Delivery Network (CDN)** : Menggunakan server di berbagai lokasi untuk mengirimkan gambar lebih cepat ke pengguna, mempercepat waktu muat.

---

## Mengapa Optimasi Gambar Penting?

Gambar adalah konten menarik di web, tapi jika lambat dimuat bisa menimbulkan masalah karena:

- **Pengalaman Pengguna yang Buruk**: Pengguna cenderung tidak menyukai website dengan gambar yang lambat.
- **Tingkat Pentalan (Bounce Rate) Tinggi**: Pengguna cenderung meninggalkan website yang lambat dimuat.
- **Penurunan Konversi**: Terutama di situs e-commerce, gambar yang lambat dapat berdampak negatif pada jumlah pembelian atau tindakan lain yang diinginkan.

Optimasi gambar membantu mengatasi masalah ini, memastikan tampilan visual yang cepat dan menarik bagi pengguna.

---

## Optimasi Gambar dengan Next.js Image Component

Next.js menyediakan **Image component** untuk mengoptimalkan performa gambar dengan berbagai fitur bawaan yang dapat membantu dalam pengelolaan gambar secara efisien.

### 1. Optimasi Ukuran (Size Optimization)

Secara otomatis dapat mengatur gambar agar sesuai dengan perangkat pengguna dan mendukung format modern seperti **WebP** dan **AVIF**. Dengan ini, gambar bisa ditampilkan dalam resolusi dan ukuran yang tepat, tanpa mengorbankan kualitas.

**Contoh Kode:**

```javascript
import Image from "next/image";

function HomePage() {
  return (
    <div>
      <h1>Contoh Gambar dengan Optimasi Ukuran</h1>
      <Image
        src="/path/to/image.jpg"
        alt="Contoh Gambar"
        width={500}
        height={300}
        quality={75}
        priority
        formats={["image/webp", "image/avif"]}
      />
    </div>
  );
}
export default HomePage;
```

**Keterangan**:

- `width` dan `height` menentukan dimensi gambar.
- `formats` mendukung format modern, seperti WebP atau AVIF, untuk mengurangi ukuran file.

---

### 2. Stabilitas Visual (Visual Stability)

Dapat mencegah **layout shift** atau pergeseran tata letak ketika gambar dimuat. Dengan menetapkan dimensi gambar terlebih dahulu, tata letak halaman tetap stabil, dan meningkatkan nilai **Cumulative Layout Shift (CLS)**.

**Contoh Kode:**

```javascript
import Image from "next/image";

function VisualStabilityExample() {
  return (
    <div>
      <h2>Contoh Gambar dengan Stabilitas Visual</h2>
      <Image
        src="/path/to/image.jpg"
        alt="Gambar Stabil"
        width={600}
        height={400}
        layout="responsive"
      />
    </div>
  );
}
export default VisualStabilityExample;
```

**Keterangan**:

- `layout="responsive"` memastikan gambar mengikuti ukuran perangkat dan menjaga dimensi awal untuk mencegah perubahan tata letak.

---

### 3. Pemuatan Halaman Lebih Cepat (Lazy Loading dan Placeholder Blur-up)

Lazy loading memungkinkan gambar hanya dimuat saat muncul di layar pengguna, sehingga menghemat bandwidth dan mempercepat waktu pemuatan halaman. **Next.js** juga mendukung **blur-up placeholders** atau placeholder buram muncul saat gambar sedang dimuat, sehingga memberikan pengalaman yang lebih halus karena gambar tidak muncul mendadak saat loading.

**Contoh Kode:**

```javascript
import Image from "next/image";

function LazyLoadExample() {
  return (
    <div>
      <h3>Contoh Gambar dengan Lazy Loading dan Placeholder Blur-up</h3>
      <Image
        src="/path/to/large-image.jpg"
        alt="Gambar Lazy Load"
        width={800}
        height={500}
        placeholder="blur"
        blurDataURL="/path/to/small-placeholder.jpg"
        loading="lazy"
      />
    </div>
  );
}
export default LazyLoadExample;
```

**Keterangan**:

- `placeholder="blur"` dan `blurDataURL` memungkinkan placeholder buram muncul sebelum gambar utama selesai dimuat.
- `loading="lazy"` mengaktifkan lazy loading untuk gambar di luar viewport.

---

### 4. Fleksibilitas Aset (On-demand Image Resizing)

Next.js dapat memungkinkan pengubahan ukuran gambar sesuai kebutuhan, baik gambar dari server internal maupun eksternal. Hal ini memudahkan pengelolaan gambar dengan berbagai resolusi tanpa harus mengubah setiap gambar secara manual.

**Contoh Kode untuk Gambar Eksternal:**

```javascript
import Image from "next/image";

function RemoteImageExample() {
  return (
    <div>
      <h4>Contoh Gambar dari Server Eksternal</h4>
      <Image
        src="https://remote-server.com/images/sample.jpg"
        alt="Gambar Remote"
        width={500}
        height={300}
        layout="intrinsic"
      />
    </div>
  );
}
export default RemoteImageExample;
```

**Keterangan**:

- `layout="intrinsic"` memastikan ukuran gambar disesuaikan dengan dimensi aslinya, baik dari server lokal maupun eksternal.

# Penggunaan Komponen `Image` di Next.js

Next.js menyediakan komponen khusus `Image` yang memungkinkan kita untuk memuat dan mengoptimalkan gambar, baik gambar lokal maupun gambar jarak jauh.

**Import Komponen `Image`**

```javascript
import Image from "next/image";
```

Anda dapat menentukan `src` untuk gambar yang Anda gunakan, baik untuk gambar lokal maupun jarak jauh.

## Menggunakan Gambar Lokal

Untuk gambar lokal, Anda bisa mengimpor file `.jpg`, `.png`, atau `.webp`. Next.js akan secara otomatis menentukan aspek rasio (`width` dan `height`) berdasarkan gambar yang diimpor. Hal ini membantu mencegah pergeseran tata letak kumulatif saat gambar dimuat.

**Contoh Penggunaan Gambar Lokal**

```javascript
// aplikasi/halaman.js
import Image from "next/image";
import profilePic from "./me.png";

export default function Page() {
  return (
    <Image
      src={profilePic}
      alt="Picture of the author"
      // width dan height disediakan secara otomatis
      // blurDataURL="data:..." juga disediakan otomatis
      placeholder="blur" // Opsional: untuk efek blur sementara
    />
  );
}
```

**Catatan**
`import` untuk gambar lokal harus dilakukan secara statis. `await import()` atau `require()` tidak didukung karena komponen `Image` perlu dianalisis pada waktu pembuatan.

### Konfigurasi `localPatterns` untuk Gambar Lokal

Anda dapat mengatur izin untuk gambar tertentu dengan menambahkan pola (`pattern`) dalam berkas `next.config.js`.

**Contoh Konfigurasi Gambar Lokal di `next.config.js`**

```javascript
module.exports = {
  images: {
    localPatterns: [
      {
        pathname: "/assets/images/**",
        search: "",
      },
    ],
  },
};
```

## Menggunakan Gambar Jarak Jauh

Untuk gambar jarak jauh, `src` diisi dengan URL gambar yang lengkap. Karena Next.js tidak memiliki akses ke file jarak jauh saat proses build, Anda perlu menentukan `width`, `height`, dan opsional `blurDataURL` secara manual.

**Contoh Penggunaan Gambar Jarak Jauh**

```javascript
import Image from "next/image";

export default function Page() {
  return (
    <Image
      src="https://s3.amazonaws.com/my-bucket/profile.png"
      alt="Gambar penulis"
      width={500}
      height={500}
    />
  );
}
```

### Konfigurasi `remotePatterns` untuk Gambar Jarak Jauh

Agar gambar dari URL tertentu dapat dioptimalkan dengan aman, tentukan pola URL yang diizinkan dalam `next.config.js`.

**Contoh Konfigurasi Gambar Jarak Jauh di `next.config.js`**

```javascript
module.exports = {
  images: {
    remotePatterns: [
      {
        protocol: "https",
        hostname: "s3.amazonaws.com",
        port: "",
        pathname: "/my-bucket/**",
      },
    ],
  },
};
```

## Pengaturan Domain

Jika Anda ingin mengoptimalkan gambar dari domain tertentu menggunakan API Optimasi Gambar bawaan Next.js, cukup tambahkan hostname di `next.config.js`.

```javascript
// next.config.js
module.exports = {
  images: {
    domains: ["s3.amazonaws.com"], // daftar domain gambar yang diizinkan
  },
};
```

## Menggunakan Loader

Loader adalah fungsi yang menghasilkan URL untuk gambar. Dengan loader, URL gambar yang Anda masukkan di `src` dapat dimodifikasi dan menghasilkan beberapa versi ukuran gambar untuk responsivitas. Next.js menyediakan loader default yang dapat mengoptimalkan gambar dari seluruh web.

**Menentukan Loader per Gambar**
Anda bisa menambahkan loader pada setiap komponen gambar untuk membuat URL gambar dari server tertentu atau CDN.

**Contoh Konfigurasi `Loader` di `next.config.js`**

```javascript
module.exports = {
  images: {
    loader: "custom",
    path: "https://example.com/myloader/",
  },
};
```

## Priority

Anda harus menambahkan properti `priority` ke gambar yang akan menjadi elemen `Largest Contentful Paint (LCP)` untuk setiap halaman. `LCP (Largest Contentful Paint)` adalah metrik yang mengukur waktu yang dibutuhkan agar elemen terbesar yang terlihat dalam viewport halaman (seperti gambar besar atau blok teks utama) muncul di layar. Semakin cepat elemen terbesar tersebut muncul, semakin baik pengalaman pengguna saat mengakses halaman web.

Dengan menambahkan properti `priority`, `Next.js` dapat memprioritaskan gambar secara khusus untuk dimuat lebih cepat (misalnya melalui tag pramuat atau petunjuk prioritas), yang akan menghasilkan peningkatan `LCP` yang signifikan.

Elemen `LCP` biasanya berupa blok teks atau gambar terbesar yang terlihat dalam viewport halaman. Saat Anda menjalankan next dev, Anda akan melihat peringatan konsol jika elemen `LCP` adalah `<Image>` tanpa properti `priority`.

Setelah Anda mengidentifikasi citra `LCP`, Anda dapat menambahkan properti seperti ini:

```javascript
import Image from "next/image";
import profilePic from "../public/me.png";

export default function Page() {
  return <Image src={profilePic} alt="Picture of the author" priority />;
}
```

Properti `priority` memastikan bahwa gambar tersebut dimuat lebih cepat, yang sangat penting untuk elemen `LCP`. Dengan menambahkan properti ini, `Next.js` akan memprioritaskan pemuatan gambar tersebut, yang dapat meningkatkan metrik `LCP` dan memberikan pengalaman pengguna yang lebih baik.

## Ukuran Gambar

Salah satu masalah umum yang dapat memperlambat kinerja situs web adalah **layout shift** (pergeseran tata letak), yaitu ketika gambar mendorong elemen lain di halaman saat memuat. Masalah ini sangat mengganggu pengguna sehingga memiliki metrik khusus yang disebut **Cumulative Layout Shift (CLS)**. Cara untuk menghindari layout shift akibat gambar adalah dengan selalu menetapkan ukuran gambar. Ini memungkinkan browser dapat mengalokasikan ruang yang cukup untuk gambar sebelum gambar tersebut dimuat.

Karena `next/image` dirancang untuk memastikan kinerja yang baik, komponen ini tidak dapat digunakan dengan cara yang dapat menyebabkan layout shift dan harus diatur ukurannya dengan salah satu dari tiga cara berikut:

1. **Otomatis**, dengan menggunakan impor statis jika Anda tahu ukuran gambar secara pasti.
2. **Manual**, Anda dapat mengatur ukuran gambar secara manual dengan menambahkan properti `width` (lebar) dan `height` (tinggi).
3. **Implisit**, dengan menggunakan `fill`, gambar akan menyesuaikan diri dengan ukuran elemen _parent_-nya.

### Bagaimana jika Saya Tidak Mengetahui Ukuran Gambar?

Jika Anda mengambil gambar dari sumber yang tidak menyediakan informasi ukuran, ada beberapa cara yang bisa dilakukan:

- Gunakan `fill`
  Properti `fill` memungkinkan gambar menyesuaikan diri dengan ukuran elemen _parent_-nya. Anda bisa menggunakan CSS untuk mengatur ukuran elemen _parent_ gambar dan mengatur properti `sizes` untuk menyesuaikan dengan berbagai ukuran layar. Anda juga bisa menggunakan `object-fit` dengan nilai `fill`, `contain`, atau `cover`, serta `object-position` untuk mengatur bagaimana gambar mengisi ruang tersebut.
- Normalisasi gambar
  Jika Anda mengontrol sumber gambar, pertimbangkan untuk mengubah pipeline gambar Anda untuk menormalisasi gambar ke ukuran tertentu.
- Modifikasi panggilan API
  Jika aplikasi Anda mengambil URL gambar melalui panggilan API (misalnya dari CMS), Anda dapat memodifikasi panggilan API untuk mengembalikan dimensi gambar bersama dengan URL.

Jika solusi-solusi di atas tidak sesuai, Anda masih dapat menggunakan elemen `<img>` standar bersama dengan komponen `next/image`.

## Styling (Penataan Gambar)

`Next.js` mendukung berbagai cara untuk styling Anda, termasuk:

- Modul CSS: Buat kelas CSS yang dicakup secara lokal untuk menghindari konflik penamaan dan meningkatkan pemeliharaan.
- CSS global: Mudah digunakan dan familiar bagi mereka yang berpengalaman dengan CSS tradisional, tetapi dapat menyebabkan kumpulan CSS yang lebih besar dan kesulitan mengelola gaya seiring dengan pertumbuhan aplikasi.
- Tailwind CSS: Kerangka kerja CSS yang mengutamakan utilitas yang memungkinkan desain kustom yang cepat dengan menyusun kelas utilitas.
- Sass: Praproses CSS populer yang memperluas CSS dengan fitur-fitur seperti variabel, aturan bersarang, dan mixin.
- CSS-in-JS: Menyematkan CSS secara langsung dalam komponen JavaScript Anda, sehingga memungkinkan penataan yang dinamis dan terskala.

Anda dapat menambahkan properti `style` ke komponen gambar untuk menyesuaikan tata letak dan tampilan gambar. Properti `style` adalah objek CSS yang berisi properti dan nilai CSS yang akan diterapkan pada gambar. Penataan komponen Gambar mirip dengan penataan `<img>` elemen normal, tetapi ada beberapa panduan yang perlu diingat:

- Gunakan `className` atau `style`, tidak styled-jsx.

  - Dalam kebanyakan kasus, kami sarankan untuk menggunakan `classNameprop`. Ini bisa berupa Modul CSS yang diimpor, stylesheet global, dll.
  - Anda juga dapat menggunakan `styleproperti` untuk menetapkan gaya sebaris.
  - Anda tidak dapat menggunakan `styled-jsx` karena cakupannya terbatas pada komponen saat ini (kecuali Anda menandai gaya tersebut sebagai global).
- Saat menggunakan `fill`, elemen induk harus memiliki `position: relative`

  - Hal ini diperlukan untuk rendering elemen gambar yang tepat dalam mode tata letak tersebut.
- Saat menggunakan `fill`, elemen induk harus memiliki `display: block`

  - Ini merupakan nilai default untuk `<div>` elemen, tetapi harus ditentukan sebaliknya.

  **Contoh Penggunaan Properti `style`**

  ```javascript
  import Image from "next/image";
  import profilePic from "../public/me.png";

  export default function Page() {
    return (
      <Image
        src={profilePic}
        alt="Picture of the author"
        style={{ borderRadius: "50%", border: "2px solid #000" }}
      />
    );
  }
  ```

## Properti

Berikut adalah ringkasan properti yang tersedia untuk komponen gambar:

| Properti              | Contoh                                     | Tipe                  | Status                | Deskripsi                                                                                                                                                                                                                                                                                                                                          |
| --------------------- | ------------------------------------------ | --------------------- | --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `src`               | `src="/profile.png"`                     | String                | Wajib                 | Sumber gambar yang akan ditampilkan.                                                                                                                                                                                                                                                                                                               |
| `width`             | `width={500}`                            | Integer (px)          | Wajib                 | Lebar gambar dalam piksel.                                                                                                                                                                                                                                                                                                                         |
| `height`            | `height={500}`                           | Integer (px)          | Wajib                 | Tinggi gambar dalam piksel.                                                                                                                                                                                                                                                                                                                        |
| `alt`               | `alt="Foto penulis"`                     | String                | Wajib                 | Teks alternatif untuk gambar, digunakan jika gambar tidak tampil.                                                                                                                                                                                                                                                                                  |
| `loader`            | `loader={imageLoader}`                   | Fungsi                | -                     | Fungsi khusus untuk memuat gambar.                                                                                                                                                                                                                                                                                                                 |
| `layout`            | `layout="fill"`                          | String                | -                     | Mengatur tata letak gambar. Nilai yang didukung:`fixed` (gambar tidak responsif), `intrinsic` (dimensi asli digunakan pada layar besar, dan diturunkan pada layar kecil), `responsive`(dimensi gambar diperbesar pada layar besar dn diperkecil pada layar kecil), dan `fill` (gambar akan memenuhi lebar dan tinggi elemen pembungkus). |
| `fill`              | `fill={true}`                            | Boolean               | -                     | Menyesuaikan gambar dengan lebar dan tinggi container secara otomatis.                                                                                                                                                                                                                                                                             |
| `sizes`             | `sizes="(max-width: 768px) 100vw, 33vw"` | String                | -                     | Pengaturan ukuran gambar yang berbeda berdasarkan lebar layar (respon gambar).                                                                                                                                                                                                                                                                     |
| `quality`           | `quality={80}`                           | Integer (1-100)       | -                     | Menentukan kualitas gambar (dari 1 hingga 100). Nilai default adalah 75.                                                                                                                                                                                                                                                                           |
| `priority`          | `priority={true}`                        | Boolean (true, false) | -                     | Menentukan prioritas pemuatan gambar lebih cepat.                                                                                                                                                                                                                                                                                                  |
| `placeholder`       | `placeholder="blur"`                     | String                | -                     | Menampilkan efek buram sementara gambar yang sedang dimuat.                                                                                                                                                                                                                                                                                        |
| `style`             | `style={{objectFit: "contain"}}`         | Object                | -                     | Menentukan gaya (style) tambahan untuk gambar, seperti `objectFit` yang mengatur bagaimana gambar sesuai dalam kontainer.                                                                                                                                                                                                                        |
| `onLoadingComplete` | `onLoadingComplete={img => done()}`      | Fungsi                | Tidak disarankan lagi | Fungsi yang dipanggil setelah gambar selesai dimuat (tidak disarankan digunakan lagi).                                                                                                                                                                                                                                                             |
| `onLoad`            | `onLoad={event => done()}`               | Fungsi                | -                     | Fungsi yang dipanggil ketika gambar selesai dimuat.                                                                                                                                                                                                                                                                                                |
| `onError`           | `onError={event => fail()}`              | Fungsi                | -                     | Fungsi yang dipanggil jika terjadi kesalahan saat memuat gambar.                                                                                                                                                                                                                                                                                   |
| `loading`           | `loading="lazy"`                         | String                | -                     | Pengaturan pemuatan gambar secara `lazy` (hanya dimuat saat diperlukan).                                                                                                                                                                                                                                                                         |
| `blurDataURL`       | `blurDataURL="data:image/jpeg..."`       | String                | -                     | Data URL yang digunakan untuk menampilkan gambar buram sebelum gambar penuh dimuat (untuk placeholder).                                                                                                                                                                                                                                            |
| `overrideSrc`       | `overrideSrc="/seo.png"`                 | String                | -                     | URL alternatif untuk menggantikan gambar asli (src) dalam situasi tertentu, seperti SEO atau performa.                                                                                                                                                                                                                                             |
