Nama: Isa Citra Buana

NPM: 2206081465

Kelas: PBP D

TUGAS 6
deployment dengan vercel: https://waifu-collection.vercel.app/
deployment dengan pbp csui: http://isa-citra-tugas.pbp.cs.ui.ac.id

1. Synchronous Programming adalah pendekatan pemrograman di mana kode dijalankan satu per satu secara hierarkis dari atas ke bawah. Itu artinya kode atau task harus menunggu kode atau task yang lebih awal untuk diselesaikan terlebih dahulu sebelum kode atau task ini dijalankan. Sementara itu, Asynchronous Programming adalah pendekatan pemrograman di mana kode dijalankan secara independen yang artinya jika kode pada baris atas belum selesai, maka kode yang berada di baris lebih bawah tidak perlu di-pending, tetapi bisa berjalan tanpa harus menunggu kode diatasnya untuk selesai. 

2. Event driven programming adalah pendekatan pemrograman di mana blok kode tertentu akan dijalankan untuk merespons event yang dilakukan oleh user. Dengan kata lain, pendekatan ini memungkinkan jalannya suatu program ditentukan oleh interaksi user terhadap program tersebut.

Contoh dari event driven programming pada tugas ini adalah:
(line 191 di home.html) 
```
<button onclick="openForm()" id="open-form-button" class=" z-20 fixed bottom-16 right-8  bg-teal-700 hover:bg-teal-500 text-black hover:text-white  rounded-md py-2 px-4 flex items-center justify-center">
<h1 class="lg:text-lg md:text-base text-xs text-white">+ Add Card</h1></button>
```
Apabila user melakukan event click terhadap button tersebut maka blok kode, dalam hal ini fungsi ``openForm`` dijalankan.
 (openForm di home.js)
 ```
 const openForm = () =>{
    const formContainerElement = document.getElementById('form-container');
    const openFormButtonElement = document.getElementById('open-form-button');
    const logoutButtonElement = document.getElementById('logout-button');
    formContainerElement.style.display = 'flex';
    openFormButtonElement.style.display = 'none';
    logoutButtonElement.style.display = 'none';
}
 ```
Begitu button dengan id ``open-form-button`` tersebut ditekan maka elemen dengan id ``form-container`` dimunculkan, sementara elemen dengan id ``open-form-button`` dan elemen dengan id ``logout-button`` disembunyikan.

3. 
Asynchronous programming dalam AJAX biasanya melibatkan penggunaan callback function. Callback function  akan dijalankan ketika permintaan berhasil (success) atau gagal (error). Terdapat konsep Promise. Promise adalah objek dalam JavaScript yang mewakili hasil dari operasi asinkron, baik itu sukses (resolved) atau gagal (rejected). Promise digunakan untuk mengelola operasi asinkron dan membuat kode yang lebih mudah dibaca dan dipahami daripada menggunakan callback. . AJAX juga menerapkan konsep async dan await untuk mengelola operasi asinkron. Ini membuat kode menjadi  lebih bersih dan mudah dipahami karena menghindari callback hell. Selain itu, penggunaan async dan await juga membuat kode lebih enak dibaca daripada menggunakan Promise.


4. Di sisi kinerja, fetch api lebih efisien daripada jquery ajax. Hal tersebut karena fetch api adalah bagian dari bawaan javascript. Dengan kata lain, fetch api adalah api yang terintegrasi secara langsung dengan browser. Sementara itu, JQuery AJAX adalah library eksternal. Hal tersebut menyebabkan JQuery AJAX memiliki overhead tambahan dibandingkan fetch api. Ketika  menggunakan jQuery AJAX, kita harus memuat seluruh library jQuery, yang termasuk banyak fitur yang mungkin tidak dibutuhkan dalam web kita. Ini berarti ada "overhead" tambahan yang terlibat dalam penggunaan jQuery hanya untuk AJAX, yang dapat memperlambat kinerja  web kita. 

Di sisi pengaturan request, fetch api memberi Anda lebih banyak kontrol langsung terhadap permintaan HTTP. Anda dapat mengelola request headers, method, respons, serta menggunakan Promise untuk mengatur logika yang lebih terperinci. Sementara itu, jQuery AJAX memberikan abstraksi yang lebih tinggi dan sederhana, yang dapat mempermudah penggunaan untuk pemula, tetapi dapat mengorbankan kontrol yang lebih halus atas permintaan dan respons HTTP.

Kemudian perbedaan lainnya adalah tentang Callback Hell. Kita bisa mengantisipasi harus menulis Callback Hell dengan fetch api yang memanfaatkan async dan await. Akan tetapi, pada jQuery AJAX, Callback Hell tidak bisa diantisipasi karena jQuery masih menggunakan penanganan Callback secara tradisional.

Saya cenderung lebih menyukai fetch api karena fetch api hingga sekarang terus dikembangkan sementara penggunaan jQuery AJAX semakin menurun. Selain itu, fetch api bisa menangani asynchronous programming secara lebih modern tanpa harus khawatir dengan Callback Hell berbeda dengan jQuery AJAX.

5.

Pertama konfigurasikan tambahkan ``'django.contrib.staticfiles'`` ke settings.py pada direktori projek.
```
...
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'main'
]
...
```
Hal ini mengaktifkan pengelolaan file static di Django.

Kemudian, pada settings.py tersebut, kita perlu mengonfigurasikan STATIC_URL dan STATIC_ROOT.
```
...
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
...
```
STATIC_URL adalah URL yang akan digunakan untuk merujuk ke file statis dalam template. STATIC_ROOT adalah direktori tempat file statis akan dikumpulkan saat menjalankan perintah collectstatic.

Kemudian, buat folder bernama static di direktori app. Dalam hal ini saya membuat folder static pada direktori main. Di dalam folder yang bernama static tersebut, tambahkan file javascript.
Saya menamai file tersebut sebagai home.js . Kemudian, tuliskan fungsi-fungsi yang kita perlukan untuk menjalankan AJAX dengan pendekatan Fetch API.
Berikut adalah kode pada main.js:
```
function getCookie(name) {
    const value = `; ${document.cookie}`;
    const parts = value.split(`; ${name}=`);
    if (parts.length === 2) return parts.pop().split(';').shift();
}
function calculateRank(strength, speed, intelligence, potential, endurance) {
    // Menghitung nilai total stats
   var totalStats = (strength + speed + intelligence + potential + endurance) / 5;

   // Menentukan kisaran rank berdasarkan total stats
   if (totalStats >= 90) {
       return 'S';
   } else if (totalStats >= 80) {
       return 'A';
   } else if (totalStats >= 70) {
       return 'B';
   } else if (totalStats >= 60) {
       return 'C';
   } else if (totalStats >= 50) {
       return 'D';
   } else {
       return 'E';
   }
}

const changeAmountAJAX = async (id, quantity) => {
    const loadingElement = document.getElementById("loadingOverlay");
    const csrftoken = getCookie('csrftoken');
    const formData = new FormData();
    formData.append('waifu_card_id', id);
    formData.append('quantity', quantity);
    try {
        loadingElement.style.display = "flex";
        const res = await fetch('/main/changeAmount/', {
            method: 'POST',
            headers: {
                'X-CSRFToken': csrftoken
            },
            body: formData
        })
        console.log(res)
        await getData()
    } catch (error) {
        console.log(error)
    }
    loadingElement.style.display = "none";
}
const deleteCardAJAX = async (id) =>{
    const loadingElement = document.getElementById("loadingOverlay");
    const csrftoken = getCookie('csrftoken');
    const formData = new FormData();
    formData.append('waifu_card_id', id);
    try {
        loadingElement.style.display = "flex";
        const res = await fetch('/main/deleteCard/', {
            method: 'POST',
            headers: {
                'X-CSRFToken': csrftoken
            },
            body: formData
        });
        console.log(res)
        await getData()
    } catch (error) {
        console.log(error)
    }
    loadingElement.style.display = "none";
}

const resetForm = () => {
    document.getElementById("name").value = "";
    document.getElementById("amount").value = "";
    document.getElementById("strength").value = 50; 
    document.getElementById("speed").value = 50;
    document.getElementById("intelligence").value = 50;
    document.getElementById("potential").value = 50;
    document.getElementById("endurance").value = 50;
    document.getElementById("description").value = "";
    document.getElementById("weight").value = ""; 
    document.getElementById("height").value = "";
    document.getElementById('strength-value').textContent = "50"; 
    document.getElementById('speed-value').textContent = "50"; 
    document.getElementById('intelligence-value').textContent = "50"; 
    document.getElementById('potential-value').textContent = "50"; 
    document.getElementById('endurance-value').textContent = "50"; 
}
const submitForm = async () =>{
    const loadingElement = document.getElementById("loadingOverlay");
    const nameInput = document.getElementById("name");
    const descriptionInput = document.getElementById("description");
    const amountInput = document.getElementById("amount");
    const weightInput = document.getElementById("weight");
    const heightInput = document.getElementById("height");
    const name = document.getElementById("name").value;
    const amount = document.getElementById("amount").value;
    const strength = document.getElementById("strength").value;
    const speed = document.getElementById("speed").value;
    const intelligence = document.getElementById("intelligence").value;
    const potential = document.getElementById("potential").value;
    const endurance = document.getElementById("endurance").value;
    const description = document.getElementById("description").value;
    const weight = document.getElementById("weight").value;
    const height = document.getElementById("height").value;

    if (name.trim() === "") {
        alert("Nama tidak boleh kosong");
        nameInput.focus();
        return false;
    }
    if (description.trim() === "") {
        alert("Deskripsi tidak boleh kosong");
        descriptionInput.focus();
        return false;
    }
    if (amount <= 0 || isNaN(amount)) {
        alert("Jumlah harus bilangan bulat lebih dari 0 dan tidak boleh kosong");
        amountInput.focus();
        return false;
    }
    if (weight <= 0 || isNaN(weight)) {
        alert("Berat harus bilangan dan tidak boleh kosong");
        weightInput.focus();
        return false;
    }
    if (height <= 0 || isNaN(height)) {
        alert("Jumlah harus bilangan dan tidak boleh kosong");
        heightInput.focus();
        return false;
    }
    const data = {
        name: name,
        description: description,
        amount: amount,
        weight: weight,
        height: height,
        strength: strength,
        speed: speed,
        intelligence: intelligence,
        potential: potential,
        endurance: endurance
    };
    try {
        loadingElement.style.display = 'flex';
        const res = await fetch('/main/create_ajax/', {
            method:"POST",
            headers: {
                'Content-Type': 'application/json'
            },
            body:JSON.stringify(data),
            
        })
        await getData()
        resetForm()

    } catch (error) {
        console.log(error)
    }
    loadingElement.style.display = 'none';
    closeForm()

}

function updateOutput(value, elementId) {
    // Mengambil elemen output
    var outputElement = document.getElementById(elementId);
    
    // Mengubah teks pada elemen output sesuai dengan nilai input
    outputElement.textContent = value;
    
}

const openForm = () =>{
    const formContainerElement = document.getElementById('form-container');
    const openFormButtonElement = document.getElementById('open-form-button');
    const logoutButtonElement = document.getElementById('logout-button');
    formContainerElement.style.display = 'flex';
    openFormButtonElement.style.display = 'none';
    logoutButtonElement.style.display = 'none';
}

const closeForm = ()=> {
    const formContainerElement = document.getElementById('form-container');
    const openFormButtonElement = document.getElementById('open-form-button');
    const logoutButtonElement = document.getElementById('logout-button');
    formContainerElement.style.display = 'none';
    openFormButtonElement.style.display = 'flex';
    logoutButtonElement.style.display = 'flex';
}

const getData = async () => {
    const containerElement = document.getElementById("collection-container");
    const totalCardElement = document.getElementById("total-of-cards");
   
    try {
        
        const res = await fetch("/main/home_ajax/");
        const {username, waifus, lastLogin, total} = await res.json();
        totalCardElement.innerHTML = `Terdapat <span  class="text-[#00A8FF]">${total} kartu waifu </span>`
        if(waifus.length == 0){
            containerElement.innerHTML = `<div class="flex w-full justify-center text-sm md:text-base lg:text-lg text-white font-bold h-full items-center">
            <h1> Belum ada waifu. Silahkan menambahkan</h1>
        </div>`
        }
        else{
            let innerHTML = `<div class="mb-4  mx-auto gap-4 grid justify-center grid-cols-1    `
            if(waifus.length == 1){
                innerHTML += `md:grid-cols-1 lg:grid-cols-1">`
            }
            else if(waifus.length == 2){
                innerHTML += `md:grid-cols-2 lg:grid-cols-2">`
            }
            else{
                innerHTML +=  `md:grid-cols-2 lg:grid-cols-3">`
            }
            waifus.forEach((waifu, index)=>{
                innerHTML+=`<div class="max-w-[24rem] bg-opacity-60 min-w-[21rem] relative w-[21rem] md:w-[24rem] px-4 mx-auto rounded-lg shadow-lg mt-2 overflow-hidden  `;
                if(index == waifus.length - 1){
                    innerHTML+= `bg-slate-700">`;
                }
                else{
                    innerHTML+= `bg-slate-950">`;
                }

                innerHTML+= `<!-- Card Header -->
                <div class="relative z-10 flex justify-between items-center w-full">
                    <div class="px-4 pt-4 flex flex-col items-center">
                        <h1 class="font-bold ml-auto text-lg text-white">Waifu <span class="text-[#00A8FF]">Card</span></h1>
                        <div class="border-b- mt-2 border-[#00A8FF] w-full mx-2"></div>
                    </div>
                    <div class="pt-4 flex items-center justify-end space-x-2">
                        <button onclick="changeAmountAJAX(${waifu.id}, -1)" class="fas fa-minus w-8 h-8" style="color: white;">
                        </button>
                        <button onclick="changeAmountAJAX(${waifu.id}, 1)" class="fas fa-plus w-8 h-8" style="color: white;">
                        </button>
                        <button onclick="deleteCardAJAX(${waifu.id})" class="fas fa-trash w-8 h-8" style="color: red;">
                        </button>
                    </div>
                </div>
                <!-- Card Body -->
                <div class="relative z-10 p-4">
                    <!-- Waifu Name & Amount -->
                    <div class="flex justify-between items-center mb-2">
                        <h2 class="text-lg font-semibold text-[#00A8FF]">${ waifu.name }</h2>
                        <div class="ml-2 text-white px-3 py-1 text-sm rounded-md bg-teal-950 hover:bg-teal-900">
                            <h1>${ waifu.amount }</h1>
                        </div>
                    </div>
                    <!-- Waifu Description -->
                    <p class="text-white text-sm" style="overflow: hidden; text-overflow: ellipsis; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical;">${ waifu.description }</p>
                    <!-- Waifu Stats -->
                    <div class="mt-4">
                        <h3 class="text-lg font-semibold text-[#00A8FF]">STATS</h3>
                        <div class="flex flex-col">
                            <div class="flex flex-col justify-center">
                                <label for="strength" class="text-white text-sm">Strength</label>
                                <div class="flex justify-between items-center">
                                    <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                                        <div class="bg-${waifu.strength <= 25 ? 'green-600' : waifu.strength <= 50 ? 'yellow-600': waifu.strength <= 75 ? 'orange-600' : 'red-600'}
                                         h-full rounded-full" style="width: ${ waifu.strength }%;"></div>
                                    </div>
                                    <span class="ml-2 text-white">${ waifu.strength }</span>
                                </div>
                            </div>
                            <div class="flex flex-col justify-center">
                                <label for="speed" class="text-white text-sm">Speed</label>
                                <div class="flex justify-between items-center">
                                    <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                                        <div class="bg-${waifu.speed <= 25 ? 'green-600' : waifu.speed <= 50 ? 'yellow-600': waifu.speed <= 75 ? 'orange-600' : 'red-600'}
                                         h-full rounded-full" style="width: ${ waifu.speed }%;"></div>
                                    </div>
                                    <span class="ml-2 text-white">${ waifu.speed }</span>
                                </div>
                            </div>
                            <div class="flex flex-col justify-center">
                                <label for="potential" class="text-white text-sm">Potential</label>
                                <div class="flex justify-between items-center">
                                    <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                                        <div class="bg-${waifu.potential <= 25 ? 'green-600' : waifu.potential <= 50 ? 'yellow-600': waifu.potential <= 75 ? 'orange-600' : 'red-600'}
                                         h-full rounded-full" style="width: ${ waifu.potential }%;"></div>
                                    </div>
                                <span class="ml-2 text-white">${ waifu.potential }</span>
                                </div>
                            </div>
                            <div class="flex flex-col justify-center">
                                <label for="intelligence" class="text-white text-sm">Intelligence</label>
                                <div class="flex justify-between items-center">
                                    <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                                        <div class="bg-${waifu.intelligence <= 25 ? 'green-600' : waifu.intelligence <= 50 ? 'yellow-600': waifu.intelligence <= 75 ? 'orange-600' : 'red-600'}
                                         h-full rounded-full" style="width: ${ waifu.intelligence }%;"></div>
                                    </div>
                                    <span class="ml-2 text-white">${ waifu.intelligence }</span>
                                </div>
                            </div>
                            <div class="flex flex-col justify-center">
                                <label for="endurance" class="text-white text-sm">Endurance</label>
                                <div class="flex justify-between items-center">
                                    <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                                        <div class="bg-${waifu.endurance <= 25 ? 'green-600' : waifu.endurance <= 50 ? 'yellow-600': waifu.endurance <= 75 ? 'orange-600' : 'red-600'}
                                         h-full rounded-full" style="width: ${ waifu.endurance }%;"></div>
                                    </div>
                                    <span class="ml-2 text-white">${ waifu.endurance }</span>
                                </div>
                            </div>
                        </div>
                    </div>
                    <!-- Waifu Physical Attributes -->
                    <div class="mt-4 flex flex-col">
                        <h3 class="text-lg font-semibold text-[#00A8FF]">Physical Attributes</h3>
                        <div class="flex justify-between items-center text-white">
                            <h1 class="text-sm">Height</h1>
                            <div class=" px-2 py-1 bg-slate-900 rounded-md text-sm">${ waifu.height } cm</div>
                        </div>
                        <div class="flex justify-between items-center text-white space-y-3">
                            <h1 class="text-sm">Weight</h1>
                            <div class=" px-2 py-1 bg-slate-900 rounded-md text-sm">${ waifu.weight } kg</div>
                        </div>
                    </div>
                </div>
                <div id="card-rank-${waifu.id}" class="z-0   w-full absolute font-bold text-[#00A8FF] opacity-30 inset-0 flex items-center justify-center text-[24rem]">
                    ${calculateRank(waifu.strength, waifu.speed, waifu.intelligence, waifu.potential,
                        waifu.endurance)}
                </div>
            </div>`
            });
            innerHTML+= `</div>`;
            containerElement.innerHTML = innerHTML;
        }

    } catch (error) {
        console.log(error)
    }
    
}
window.addEventListener('DOMContentLoaded', async ()=> {
    const loadingElement = document.getElementById("loadingOverlay");
    loadingElement.style.display = 'flex';
    await getData();
    loadingElement.style.display = 'none';
})
```
Kemudian, kita perlu memodifikasi template home.html . Kita perlu menambahkan ``{% load static %}`` pada bagian atas file tersebut setelah `` {% extends 'base.html' %}``.
Selanjutnya di ujung bawah tepat sebelum ``  {% endblock content %}`` , kita harus membuat elemen script yang sourcenya mengacu kepada home.js  agar kita bisa menjalankan kode-kode yang ada di dalamnya. Caranya adalah dengan menambahkan ``<script src="{% static 'home.js' %}"></script>``. 

Selain itu, ada hal yang perlu kita lakukan. Yaitu menambahkan id ke setiap elemen yang akan dirujuk di file home.js tersebut. Hal tersebut karena untuk merujuk ke elemen html tersebut, kita bisa menggunakan salah satu method pada DOM yaitu getElementById untuk merujuk ke elemen html tertentu berdasarkan idnya.

Untuk memodifikasi tampilan elemen yang kita rujuk, apabila elemen tersebut berfungsi sebagai container, maka biasanya kita akan memodifikasi innerHTML nya dengan memodifikasi field innerHTML denggan men-assign value yang sesuai. Sementara itu, jika ingin memodifikasi text pada elemen, kita bisa memodifikasi field textContent dengan men-assign value yang sesuai. Apabila kita ingin memodifikasi gaya elemen tersebut, kita bisa mengakses field-field yang berada di field style dari objek elemen tersebut dan men-assign value yang sesuai.


TUGAS 5

deployment: https://waifu-collection.vercel.app/

1. Elemen selector dapat dimanfaatkan untuk mengatur gaya default dari setiap elemen html. Misalnya ketika kita ingin mendesain elemen ``<pre></pre>`` agar memiliki bentuk kotak dengan background hitam dengan teks berwarna putih , maka kita dapat memanfaatkan elemen selector tersebut seperti ini:
```
pre {
	background-color:black;
	padding: 0.5rem;
	color:white
}
```
Waktu yang tepat untuk menggunakan elemen selector adalah ketika kita ingin memberikan default style untuk setiap elemen html dengan tipe tertentu.
Selain terdapat elemen selector, masih ada beberapa selector lain. Contohnya adalah Id selector, class selector, dan Universal selector.
Id selector adalah selector yang digunakan untuk memilih elemen html berdasarkan attribut Idnya. Cara menggunakannyaa adalah dengan diawali tanda jangkar "#", lalu dilanjutkan nama idnya lalu kurung kurawal dan tuliskan style di dalam kurung kurawal tersebut.
Contoh:
```
#special-pre {
	background-color:black;
	padding: 0.5rem;
	color:white
}
```
Waktu yang tepat untuk menggunakan id selector adalah ketika ingin memberikan style terpersonalisasi untuk suatu elemen html.
Class selector adalah selector yang digunakan untuk memilih setiap elemen html dengan kelas tertentu. Cara menggunakannya adalah dengan diawali tanda titik ".", lalu dilanjutkan nama classnya lalu kurung kurawal dan tuliskan style di dalam kurung kurawal tersebut.
Contoh:
```
.my-pre{
	background-color:black;
	padding: 0.5rem;
	color:white
}
```
Universal selector adalah selector yang memilih semua elemen html yang ada. Cara menggunakannya adalah dengan diawali tanda bintang "*", lalu dilanjutkan dengan kurung kurawal dan tuliskan style di dalam kurung kurawal tersebut.
Contoh:
```
*{
	background-color:black;
	color:white
}
```
Waktu yang teoat untuk menggunakan universal selector adalah ketika kita ingin mengaplikasikan style-style dasar untuk html kita.

2.
``<header></header>``
Dapat digunakan untuk membungkus judul web dan navigation bar. Digunakan bersama dengan tag <nav></nav>
``<nav></nav>``
Dapat digunakan sebagai container untuk navigation bar.
``<section></section>``
Biasa digunakan untuk elemen yang membungkus section suatu artikel dan diberikan id unik sehingga bisa diakses dan dinavigasikan langsung ke section  yang terkait melalui table of content.
``<article></article>``
Biasa digunakan untuk mengelompokkan konten yang berdiri sendiri atau artikel yang bisa berdiri sendiri dalam halaman web.
``<aside></aside>``
Bisa digunakan untuk mengelompokkan konten tambahan yang terkait dengan konten utama di halaman web, seperti sidebar atau catatan samping.
``<main></main>``
Biasa digunakan untuk mengidentifikasi konten utama dari halaman web. Hanya satu elemen <main> yang diperbolehkan dalam satu halaman.
``<footer></footer>``
Biasa digunakan untuk mendefinisikan bagian footer dari suatu elemen atau halaman web. Biasanya digunakan untuk informasi kontak, hak cipta, atau tautan-tautan terkait lainnya. Biasanya footer ditempatkan di bagian paling bawah dari halaman web
``<figure></figure>``
Tag ini digunakan untuk mengelompokkan konten multimedia, seperti gambar atau video, dengan keterangan yang terkait menggunakan tag <figcaption>.
``<figcaption></figcaption>``
Tag ini digunakan dalam hubungannya dengan tag <figure> untuk memberikan keterangan atau deskripsi pada konten multimedia.
``<video>``
Digunakan untuk menampilkan video dalam halaman web. Agar tag ini dapat digunakan kita perlu mengisi atribut src dengan link atau url video.
``<audio>``
Digunakan untuk menampilkan audio dalam halaman web. Agar tag ini dapat digunakan kita perlu mengisi atribut src dengan link atau url audio.
``<canvas></canvas>``
Tag ini digunakan untuk membuat gambar atau grafik interaktif menggunakan JavaScript.
``<input>``
Tag ini digunakan untuk membuat berbagai jenis elemen masukan, seperti kotak teks, tombol radio, atau kotak centang.
``<textarea></textarea>``
Tag ini digunakan untuk membuat area teks yang lebih besar yang memungkinkan pengguna memasukkan teks dalam jumlah yang lebih besar.
``<a></a>``
Tag ini digunakan untuk membuat tautan atau hyperlink.
``<img>``
Tag ini digunakan untuk menampilkan gambar dalam halaman web.
``<ul></ul>, <ol></ol>, <li></li>``
``<ol></ol>`` digunakan untuk membuat unordered list. ``<ul></ul>`` digunakan untuk membuat ordered list.  ``<li></li>`` digunakan untuk membuat item dari list tersebut
``<div></div>``
Tag ini digunakan untuk mengelompokkan elemen-elemen HTML dan sering digunakan dalam styling dan tata letak halaman web.
``<span></span>``
Digunakan untuk mengelompokkan sebagian kecil teks atau elemen dalam dokumen. Dalam paragraf biasanya digunakan untuk mengelompokkan bagian dari paragraf tersebut yang akan di-style berbeda.
``<form></form>``
Digunakan untuk membuat formulir yang memungkinkan pengguna memasukkan data atau mengirim data ke server dengan GET,POST, atau request lainnya.
``<iframe>``
Tag ini digunakan untuk menampilkan halaman web atau konten dari sumber eksternal dalam halaman web.

3. Margin adalah jarak antara suatu elemen dengan elemen lainnya yang diukur dari batas elemen tersebut. Sementara itu, padding adalah jarak antara batas elemen dengan konten elemen itu sendiri. Bisa dibilang margin adalah ruang kosong diantara elemen-elemen, sementara padding adalah ruang kosong didalam suatu elemen yang berada di antara batas elemen dengan konten elemen.

4. Bootstrap cocok digunakan untuk proyek-proyek web yang membutuhkan desain yang konsisten, sementara tailwind cocok untuk proyek web yang membutuhkan banyak kustomisasi tampilan. Bootstrap juga lebih cocok untuk pemula yang baru terjun ke dunia web karena bootstrap sudah menyediakan komponen-komponen siap pakai , berbeda dengan tailwind yang lebih cocok digunakan oleh orang yang sudah terbiasa dalam dunia web karena kelas utilitas yang dimiliki tailwind adalah simplifikasi penulisan dari kombinasi sintaks CSS yang rumit.
   
5. Untuk menerapkan kustomisasi pada aplikasi django kita, hal pertama yang saya lakukan adalah dengan menambahkan link css atau script cdn dari framework css tertentu ke dalam base.html kita. Mengapa demikian? Karena di Django, selain simple, di Django juga sepertinya agak sulit untuk menginstal post-css dari framework css. Untuk itu saya menambahkan script cdn tailwind, yaitu <script src="https://cdn.tailwindcss.com"></script> ini ke dalam base.html yang berada di folder templates pada
```
{% load static %}
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta
            name="viewport"
            content="width=device-width, initial-scale=1.0"
        />
        <script src="https://cdn.tailwindcss.com"></script>


        {% block meta %}
        {% endblock meta %}
    </head>


    <body class="bg-slate-900">
        {% block content %}
        {% endblock content %}
    </body>
</html>
```
Hal itu memungkinkan cdn tersebut bisa diakses di template yang melakukan extends terhadap base.html.

Untuk menerapkan kelas tailwind ke login.html, pastikan bahwa kita telah melakukan extends terhadap base.html pada login.html kita. Selanjutnya, kita dapat menerapkan kelas-kelas tailwind tersebut dengan menuliskan kelas-kelas tersebut ke atribut kelas dari elemen yang ingin kita modifikasi tampilannya. Kemudian, apabila kita ingin menambahkan kustomisasi terhadap kotak login yang berada di Django, sebaiknya kita berhentikan menggunakan {{form.as_p}} atau {{form.as_table}}. Hal tersebut karena akan sangat sulit untuk mengkustomisasinya. Sebagai gantinya, sebaiknya kita membuat form dengan input-inputnya secara manual dan kemudian menambahkan kelas tailwind yang sesuai ke elemen form dan input tersebut. Saya melakukannya seperti ini:
```
{% extends 'base.html' %}
{% block meta %}
  <title>Masuk ke Akun Waifu</title>
   
{% endblock meta %}
{% block content %}
<div id="loadingOverlay" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50">
  
  <div role="status" class="bg-white bg-opacity-50 rounded-lg p-4 shadow-lg flex justify-center items-center">
    <svg aria-hidden="true" class="w-10 h-10 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z" fill="currentColor"/>
      <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z" fill="currentFill"/>
    </svg>
  </div>
</div>
<div class=" hidden md:flex fixed right-0 top-0 h-screen w-3/4 bg-blue-700 -z-20" style="clip-path: polygon(100% 0%, 100% 100%, 0% 100%, 80% 0%);">
</div>

<div class=" min-h-screen overflow-y-auto flex flex-col justify-center items-center w-screen">
  <div class="mb-4 flex font-bold w-full text-white lg:text-4xl md:text-2xl text-xl">
    <h1 class=" mx-auto">Login Akun <span class="text-[#00A8FF]">Waifu Kamu</span> </h1>
  </div>
  <form class="flex flex-col min-h-[28rem] bg-slate-950 px-4 py-2 rounded-md text-white max-w-[95%] min-w-[18rem] md:w-[28rem] w-[24rem]" autocomplete="off" method="post">
    {% csrf_token %}
    <div class="mb-4">
      <label for="username" class="block text-white text-sm mb-2">Username</label>
      <input autocomplete="off" required type="text" name="username" class=" bg-slate-800 focus:border text-white text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" placeholder="Masukkan nama kamu" id="username">
    </div>
    <div class="mb-4">
      <label for="password" class="block text-white text-sm mb-2">Password</label>
      <input autocomplete="off" required type="password" name="password" class="bg-slate-800 focus:border text-white text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" placeholder="Buat password" id="password">
    </div>
    <div class="mb-4">
      <h1 class="block text-white text-sm mb-2">Belum punya akun? <span><a href="{% url 'main:register' %}" class="font-bold text-[#00A8FF]">Register</a></span></h1>
    </div>  
    <div class="mb-4 mt-auto">
      <hr class=" border-2 rounded-md border-[#00A8FF]">
    </div>
    <div class="mb-2 w-full  text-sm flex">
      <button onclick="onSubmit()" class="ml-auto px-4 py-2 bg-[#00A8FF] text-black hover:text-white hover:bg-blue-900 rounded-sm"type="submit">Masuk</button>
    </div>
     
  </form>
</div>
<script>
const myElement = document.getElementById('loadingOverlay');


window.addEventListener('load', function() {
  myElement.style.display = 'none';
});
function onSubmit (){
myElement.style.display = 'flex';
setTimeout(function() {
  myElement.style.display = 'none';
}, 5000);
}
</script>
{% endblock content %}
```
Untuk menerapkan kelas tailwind ke register.html, mirip seperti kita melakukannya pada login.html, pastikan bahwa kita telah melakukan extends terhadap base.html pada register.html kita. Selanjutnya, kita dapat menerapkan kelas-kelas tailwind tersebut dengan menuliskan kelas-kelas tersebut ke atribut kelas dari elemen yang ingin kita modifikasi tampilannya. Kemudian, apabila kita ingin menambahkan kustomisasi terhadap kotak login yang berada di Django, sebaiknya kita berhentikan menggunakan {{form.as_p}} atau {{form.as_table}}. Hal tersebut karena akan sangat sulit untuk mengkustomisasinya. Sebagai gantinya, sebaiknya kita membuat form dengan input-inputnya secara manual dan kemudian menambahkan kelas tailwind yang sesuai ke elemen form dan input tersebut. Saya melakukannya seperti ini:

```
{% extends 'base.html' %}
{% block meta %}
  <title>Register</title>
   
{% endblock meta %}
{% block content %}
<div id="loadingOverlay" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50">
  
  <div role="status" class="bg-white bg-opacity-50 rounded-lg p-4 shadow-lg flex justify-center items-center">
    <svg aria-hidden="true" class="w-10 h-10 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z" fill="currentColor"/>
      <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z" fill="currentFill"/>
    </svg>
  </div>
</div>
<div class=" hidden md:flex fixed right-0 top-0 h-screen w-3/4 bg-blue-700 -z-20" style="clip-path: polygon(100% 0%, 100% 100%, 0% 100%, 80% 0%);">
</div>

<div class=" min-h-screen overflow-y-auto flex flex-col justify-center items-center w-screen">
  <div class="mb-4 flex font-bold w-full text-white lg:text-4xl md:text-2xl text-xl">
    <h1 class=" mx-auto">Buat Akun <span class="text-[#00A8FF]">Waifu Baru</span> </h1>
  </div>
  <form class="flex flex-col min-h-[28rem] bg-slate-950 px-4 py-2 rounded-md text-white max-w-[95%] min-w-[20rem] md:w-[28rem] w-[24rem]" autocomplete="off" method="post">
    {% csrf_token %}
    <div class="mb-4">
      <label for="{{ form.username.id_for_label }}" class="block text-white text-sm mb-2">Username</label>
      <input type="text" name="username" class=" bg-slate-800 focus:border text-white text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" placeholder="Masukkan nama kamu" id="{{ form.username.id_for_label }}">
      <p class="mt-2 text-[#00A8FF] text-xs text-justify">Required. 150 characters or fewer. Letters, digits and @/./+/-/_ only.</p>
    </div>
    <div class="mb-4">
      <label for="{{ form.password1.id_for_label }}" class="block text-white text-sm mb-2">Password</label>
      <input type="password" name="password1" class="bg-slate-800 focus:border text-white text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" placeholder="Buat password" id="{{ form.password1.id_for_label }}">
      <p class="mt-2 text-[#00A8FF] text-xs text-justify">Your password can`t be too similar to your other personal information.
        Your password must contain at least 8 characters.
        Your password can`t be a commonly used password.
        Your password can`t be entirely numeric.</p>
    </div>
    <div class="mb-4">
      <label for="{{ form.password2.id_for_label }}" class="block text-white text-sm mb-2">Confirm Password</label>
      <input type="password" name="password2" class="bg-slate-800 focus:border text-white text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"placeholder="Ulangi password" id="{{ form.password2.id_for_label }}">
      <p class="mt-2 text-[#00A8FF] text-xs text-justify">Enter the same password as before, for verification.</p>
    </div>
    <div class="mb-4">
      <h1 class="block text-white text-sm mb-2">Sudah punya akun? <span><a href="{% url 'main:login' %}" class="font-bold text-[#00A8FF]">Login</a></span></h1>
    </div>  
    <div class="mb-4 mt-auto">
      <hr class=" border-2 rounded-md border-[#00A8FF]">
    </div>
    <div class="mb-2 w-full  text-sm flex">
      <button onclick="onSubmit()" class="ml-auto px-4 py-2 bg-[#00A8FF] text-black hover:text-white hover:bg-blue-900 rounded-sm"type="submit">Buat Akun</button>
    </div>
     
  </form>
   
</div>
<script>
const myElement = document.getElementById('loadingOverlay');
window.addEventListener('load', function() {
  myElement.style.display = 'none';
});
function onSubmit (){
myElement.style.display = 'flex';
setTimeout(function() {
  myElement.style.display = 'none';
}, 5000);
}
</script>
{% endblock content %}
```

Untuk menerapkan kelas tailwind ke addCard.html, mirip seperti kita melakukannya pada cara yang sebelumnya, pastikan bahwa kita telah melakukan extends terhadap base.html pada addCard.html kita. Selanjutnya, kita dapat menerapkan kelas-kelas tailwind tersebut dengan menuliskan kelas-kelas tersebut ke atribut kelas dari elemen yang ingin kita modifikasi tampilannya. Kemudian, apabila kita ingin menambahkan kustomisasi terhadap kotak login yang berada di Django, sebaiknya kita berhentikan menggunakan {{form.as_p}} atau {{form.as_table}}. Hal tersebut karena akan sangat sulit untuk mengkustomisasinya. Sebagai gantinya, sebaiknya kita membuat form dengan input-inputnya secara manual dan kemudian menambahkan kelas tailwind yang sesuai ke elemen form dan input tersebut. Saya melakukannya seperti ini:
```
{% extends 'base.html' %}
{% block meta %}
<title>Tambah Kartu</title>
{% endblock meta %}
{% block content %}
<div id="loadingOverlay" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50">
  
  <div role="status" class="bg-white bg-opacity-50 rounded-lg p-4 shadow-lg flex justify-center items-center">
    <svg aria-hidden="true" class="w-10 h-10 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z" fill="currentColor"/>
      <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z" fill="currentFill"/>
    </svg>
  </div>
</div>
<div class=" hidden md:flex fixed right-0 top-0 h-screen w-3/4 bg-blue-700 -z-20" style="clip-path: polygon(100% 0%, 100% 100%, 0% 100%, 80% 0%);">
</div>
<div class="hidden fixed md:flex justify-end items-end w-screen h-screen -z-10 ">
  <img class=" w-96 h-auto"src="https://firebasestorage.googleapis.com/v0/b/isa-citra-1691878861005.appspot.com/o/marin-svg.svg?alt=media&token=4260c0db-77af-4631-b748-c1d562032baa" alt="">
</div>
<div class=" w-screen min-h-screen flex lg:-ml-8 justify-center lg:justify-center md:justify-start items-center text-white">
  <div class= "flex flex-col items-center">
    <h1 class="mt-6 text-white text-4xl font-bold font-sans"> Tambah <span class="text-[#00A8FF]">Kartu Waifu</span></h1>
    <div class=" mt-4 md:mt-8 bg-slate-950 px-4 max-w-[95%] mx-2 md:min-w-[36rem] py-2 rounded-md">
      <form method="POST" action="">
        {% csrf_token %}
        
        <div class=" grid grid-cols-4 gap-4">
        <div class=" flex-col flex md:col-span-2 col-span-3">
          <label for="name" class=" text-white mb-2 text-sm">Nama Waifu</label>
          <input for="name" name="name" id="name" class="bg-slate-800 focus:border text-white text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" type="text" placeholder="Nama waifu idamanmu" required>
        </div>
        <div class="mb-2 md:col-span-2 col-span-1">
          <label for="amount" class="block text-white text-sm mb-2">Amount</label>
          <input
          required
            type="number"
            id="amount"
            name="amount"
            min="1"
            max="100"
            step="1"
            placeholder="Jumlah"
            class="bg-slate-800 focus:border text-white text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
          >
        </div>
        </div>
        <div class=" grid-cols-2 md:grid gap-4">

          <div class=" flex flex-col">
            <label class="mt-2 mb-2 text-sm" for="strength">Strength</label>
            <div class=" flex justify-between">
              <input
            required
            class =" w-[90%]"
            type="range"
            id="strength"
            name="strength"
            min="1"
            max="100"
            step="1"
            value="50"
            oninput="updateOutput(this.value, 'strength-value'); "
            >
            <output for="strength" id="strength-value">50</output>
            </div>
          </div>

          <div class=" flex flex-col">
            <label class="mt-2 mb-2 text-sm" for="speed">Speed</label>
            <div class=" flex justify-between">
              <input
            required
            class =" w-[90%]"
            type="range"
            id="speed"
            name="speed"
            min="1"
            max="100"
            step="1"
            value="50"
            oninput="updateOutput(this.value, 'speed-value'); "
            >
            <output for="speed" id="speed-value">50</output>
            </div>
          </div>

          <div class=" flex flex-col">
            <label class="mt-2 mb-2 text-sm" for="intelligence">Intelligence</label>
            <div class=" flex justify-between">
              <input
            required
            class =" w-[90%]"
            type="range"
            id="intelligence"
            name="intelligence"
            min="1"
            max="100"
            step="1"
            value="50"
            oninput="updateOutput(this.value, 'intelligence-value')"
            >
            <output for="intelligence" id="intelligence-value">50</output>
            </div>
          </div>

          <div class=" flex flex-col">
            <label class="mt-2 mb-2 text-sm" for="potential">Potential</label>
            <div class=" flex justify-between">
              <input
            required
            class =" w-[90%]"
            type="range"
            id="potential"
            name="potential"
            min="1"
            max="100"
            step="1"
            value="50"
            oninput="updateOutput(this.value, 'potential-value');"
            >
            <output for="potential" id="potential-value">50</output>
            </div>
          </div>
          <div class=" flex flex-col">
            <label class="mt-2 mb-2 text-sm" for="endurance">Endurance</label>
            <div class=" flex justify-between">
              <input
            required
            class =" w-[90%]"
            type="range"
            id="endurance"
            name="endurance"
            min="1"
            max="100"
            step="1"
            value="50"
            oninput="updateOutput(this.value, 'endurance-value');"
            >
            <output for="endurance" id="endurance-value">50</output>
            </div>
          </div>
          
        </div>
        <div class="flex flex-col">
          <label for="description" class=" text-white mb-2 mt-2 text-sm">Deskripsi</label>
          <textarea required id="description" for="description"name="description" class="bg-slate-800 focus:border text-white text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" type="text" placeholder="Deskripsi tentang waifumu"></textarea>
        </div>
        <div class=" grid grid-cols-2 gap-4 mt-2">
          <div class="flex flex-col">
            <label for="weight" class="block text-white text-sm mb-2">Weight (kg)</label>
          <input
            required
            type="number"
            id="weight"
            name="weight"
            min="1"
            max="100"
            step="0.5"
            placeholder="Berat Waifu-mu"
            class="bg-slate-800 focus:border text-white text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
          >
          </div>
          <div class="flex flex-col">
            <label for="amount" class="block text-white text-sm mb-2">Height (cm)</label>
          <input
            required
            type="number"
            id="height"
            name="height"
            min="1"
            max="200"
            step="0.5"
            placeholder="Tinggi waifu-mu"
            class="bg-slate-800 focus:border text-white text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
          >
          </div>
        </div>
        <div class="flex mt-4">
          <input type="submit" value="Tambah Kartu" onclick="onSubmit()" class="ml-auto px-4 py-2 text-sm rounded-md bg-slate-900 hover:bg-slate-800">
        </div>
      </form>
    </div>
  </div>
</div>

<script>
  const myElement = document.getElementById('loadingOverlay');


    window.addEventListener('load', function() {
      myElement.style.display = 'none';
    });
  function onSubmit (){
    myElement.style.display = 'flex';
    setTimeout(function() {
      myElement.style.display = 'none';
    }, 5000);
  }
  function updateOutput(value, elementId) {
    // Mengambil elemen output
    var outputElement = document.getElementById(elementId);
     
    // Mengubah teks pada elemen output sesuai dengan nilai input
    outputElement.textContent = value;
  }
</script>
{% endblock content %}
```

Sama seperti sebelumnya, hal yang perlu kita lakukan pertama kali untuk mendesain tampilan home.html adalah dengan meng-extends base.html pada home.html. Untuk selanjutnya, karena kita fokus untuk merender card, kita bisa buat desain cardnya akan seperti apa. Di sini saya membuat desain cardnya seperti ini:
```
<div class="max-w-[24rem] min-w-[21rem] relative w-[21rem] md:w-[24rem] px-4 mx-auto bg-slate-950 rounded-lg shadow-lg mt-2 overflow-hidden">
        <!-- Card Header -->
         
        <div class="relative z-10 flex justify-between items-center w-full">
          <div class="px-4 pt-4 flex flex-col items-center">
            <h1 class="font-bold ml-auto text-lg text-white">Waifu <span class="text-[#00A8FF]">Card</span></h1>
            <div class="border-b- mt-2 border-[#00A8FF] w-full mx-2"></div>
          </div>
          <div class="pt-4 flex items-center justify-end space-x-2">
            <button onclick="changeAmount({{data.id}}, -1)" class="fas fa-minus w-8 h-8" style="color: white;">
            </button>
            <button onclick="changeAmount({{data.id}}, 1)" class="fas fa-plus w-8 h-8" style="color: white;">
            </button>
            <button onclick="deleteCard({{data.id}})" class="fas fa-trash w-8 h-8" style="color: red;">
            </button>
          </div>
           
        </div>
        <!-- Card Body -->
        <div class="relative z-10 p-4">
          <!-- Waifu Name & Amount -->
          <div class="flex justify-between items-center mb-2">
            <h2 class="text-lg font-semibold text-[#00A8FF]">{{ data.name }}</h2>
            <div class="ml-2 text-white px-3 py-1 text-sm rounded-md bg-teal-950 hover:bg-teal-900">
              <h1>{{ data.amount }}</h1>
            </div>
          </div>
          <!-- Waifu Description -->
          <p class="text-white text-sm" style="overflow: hidden; text-overflow: ellipsis; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical;">{{ data.description }}</p>
          <!-- Waifu Stats -->
          <div class="mt-4">
            <h3 class="text-lg font-semibold text-[#00A8FF]">STATS</h3>
            <div class="flex flex-col">
              <div class="flex flex-col justify-center">
                <label for="strength" class="text-white text-sm">Strength</label>
                <div class="flex justify-between items-center">
                  <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                    <div class="bg-{% if data.strength <= 25 %}green-600{% elif data.strength <= 50 %}yellow-600{% elif data.strength <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.strength }}%;"></div>
                  </div>
                  <span class="ml-2 text-white">{{ data.strength }}</span>
                </div>
              </div>
              <div class="flex flex-col justify-center">
                <label for="speed" class="text-white text-sm">Speed</label>
                <div class="flex justify-between items-center">
                  <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                    <div class="bg-{% if data.speed <= 25 %}green-600{% elif data.speed <= 50 %}yellow-600{% elif data.speed <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.speed }}%;"></div>
                  </div>
                  <span class="ml-2 text-white">{{ data.speed }}</span>
                </div>
              </div>
              <div class="flex flex-col justify-center">
                <label for="potential" class="text-white text-sm">Potential</label>
                <div class="flex justify-between items-center">
                  <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                    <div class="bg-{% if data.potential <= 25 %}green-600{% elif data.potential <= 50 %}yellow-600{% elif data.potential <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.potential }}%;"></div>
                  </div>
                <span class="ml-2 text-white">{{ data.potential }}</span>
                </div>
              </div>
              <div class="flex flex-col justify-center">
                <label for="intelligence" class="text-white text-sm">Intelligence</label>
                <div class="flex justify-between items-center">
                  <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                    <div class="bg-{% if data.intelligence <= 25 %}green-600{% elif data.intelligence <= 50 %}yellow-600{% elif data.intelligence <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.intelligence }}%;"></div>
                  </div>
                  <span class="ml-2 text-white">{{ data.intelligence }}</span>
                </div>
              </div>
              <div class="flex flex-col justify-center">
                <label for="endurance" class="text-white text-sm">Endurance</label>
                <div class="flex justify-between items-center">
                  <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                    <div class="bg-{% if data.endurance <= 25 %}green-600{% elif data.endurance <= 50 %}yellow-600{% elif data.endurance <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.endurance }}%;"></div>
                  </div>
                  <span class="ml-2 text-white">{{ data.endurance }}</span>
                </div>
              </div>
            </div>
          </div>
          <!-- Waifu Physical Attributes -->
          <div class="mt-4 flex flex-col">
            <h3 class="text-lg font-semibold text-[#00A8FF]">Physical Attributes</h3>
            <div class="flex justify-between items-center text-white">
              <h1 class="text-sm">Height</h1>
              <div class=" px-2 py-1 bg-slate-900 rounded-md text-sm">{{ data.height }} cm</div>
            </div>
            <div class="flex justify-between items-center text-white space-y-3">
              <h1 class="text-sm">Weight</h1>
              <div class=" px-2 py-1 bg-slate-900 rounded-md text-sm">{{ data.weight }} kg</div>
            </div>
          </div>
        </div>
        <div id="card-rank-{{data.id}}" class="z-0  w-full absolute font-bold text-[#00A8FF] opacity-30 inset-0 flex items-center justify-center text-[24rem]">
          A
        </div>
        <script>
          function calculateRank(strength, speed, intelligence, potential, endurance) {
             // Menghitung nilai total stats
            var totalStats = (strength + speed + intelligence + potential + endurance) / 5;

            // Menentukan kisaran rank berdasarkan total stats
            if (totalStats >= 90) {
              return 'S';
            } else if (totalStats >= 80) {
              return 'A';
            } else if (totalStats >= 70) {
              return 'B';
            } else if (totalStats >= 60) {
              return 'C';
            } else if (totalStats >= 50) {
              return 'D';
            } else {
              return 'E';
            }
          }  
          var element = document.getElementById("card-rank-{{ data.id }}");
          var strength = {{ data.strength }};
          var speed = {{ data.speed }};
          var intelligence = {{ data.intelligence }};
          var potential = {{ data.potential }};
          var endurance = {{ data.endurance }};
          if(element){
            console.log('here')
            element.innerText = calculateRank(strength, speed, intelligence, potential, endurance)
          }
        </script>
      </div>
```
Kemudian setelah itu, kita perlu merender bagaimana card tersebut diposisikan, nah saya sendiri ingin memposisikan bahwa card-card tersebut ditampilkan 1 kolom jika layar berukuran kecil, 2 kolom jika layar tersebut berukuran medium, 3 kolom jika layar berukuran besar. Untuk itu, saya memanfaatkan grid system dari tailwind.

Untuk desain layout kira kira seperti ini:
```
 {% if waifus|length == 0 %}
      <div class="flex w-full justify-center text-sm md:text-base lg:text-lg text-white font-bold h-full items-center">
        <h1> Belum ada waifu. Silahkan menambahkan</h1>
      </div>
    {% else %}
      <div class="mb-4 mx-auto gap-4 grid grid-cols-1 {% if waifus|length == 1 %}md:grid-cols-1 lg:grid-cols-1{% elif waifus|length == 2 %}md:grid-cols-2 lg:grid-cols-2{% else %}md:grid-cols-2 lg:grid-cols-3{% endif %} justify-center ">
<!--Render Seluruh Card -->
{% endif %}
```
Kemudian kita padukan kedua hal tersebut (desain card dan layoutnya) dengan elemen-elemen lain maupun script untuk menghasilkan hasil final home.html seperti ini:
```
{% extends 'base.html' %}


  {% block meta %}
  <title>Waifu Card Collection</title>
   
  {% endblock meta %}
   
  {% block content %}
   
<div id="loadingOverlay" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50">
  
  <div role="status" class="bg-white bg-opacity-50 rounded-lg p-4 shadow-lg flex justify-center items-center">
    <svg aria-hidden="true" class="w-10 h-10 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z" fill="currentColor"/>
      <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z" fill="currentFill"/>
    </svg>
  </div>
</div>

  <div class="w-screen min-h-screen overflow-y-auto flex flex-col">
     
    <div class=" hidden md:flex fixed right-0 top-0 h-screen w-3/4 bg-blue-700 -z-20" style="clip-path: polygon(100% 0%, 100% 100%, 0% 100%, 80% 0%);">
    </div>
    <a href="{% url 'main:logout' %}" onclick="onLogout()" class="fixed top-2 right-2 text-white px-4 py-2 text-base rounded-md bg-slate-950 hover:bg-teal-900">
      <h1>Logout</h1>
    </a>
    <a href="{% url 'main:addCard' %}" onclick="onClickAdd()" class=" z-20 fixed bottom-24 right-12 md:right-24 bg-[#00A8FF] hover:bg-teal-700 text-black hover:text-white rounded-full md:w-16 md:h-16 w-12 h-12 flex items-center justify-center">
      <h1 class="text-4xl font-bold mb-1">+</h1>
    </a>
    <div class="flex flex-col w-full text-base p-4 text-white font-bold ">
      <div class=" p-4 rounded-md bg-opacity-30 text-base">
        <h1>Nama Aplikasi: <span class="text-[#00A8FF]">Waifu Card Collection</span></h1>
      <h1>Nama: <span class="text-[#00A8FF]">Isa Citra Buana</span></h1>
      <h1>NPM: <span class="text-[#00A8FF]">2206081465</span></h1>
      <h1>Kelas: <span class="text-[#00A8FF]">PBP D</span></h1>
      </div>
      <div class="flex w-full mb-2 justify-center text-base text-white font-bold h-full items-center">
        <h1> <span class="text-[#00A8FF]">{{username}}</span> terakhir login pada {{last_login}}</h1>
      </div>
      <div class=" mx-auto text-white font-bold text-base ">
        <h1>Terdapat <span class="text-[#00A8FF]">{{total}} kartu waifu </span></h1>
      </div>

    </div>
     
     
    {% if waifus|length == 0 %}
      <div class="flex w-full justify-center text-sm md:text-base lg:text-lg text-white font-bold h-full items-center">
        <h1> Belum ada waifu. Silahkan menambahkan</h1>
      </div>
    {% else %}
      <div class="mb-4 mx-auto gap-4 grid grid-cols-1 {% if waifus|length == 1 %}md:grid-cols-1 lg:grid-cols-1{% elif waifus|length == 2 %}md:grid-cols-2 lg:grid-cols-2{% else %}md:grid-cols-2 lg:grid-cols-3{% endif %} justify-center ">
      {% for data in waifus %}
      <div class="max-w-[24rem] min-w-[21rem] relative w-[21rem] md:w-[24rem] px-4 mx-auto bg-slate-950 rounded-lg shadow-lg mt-2 overflow-hidden">
        <!-- Card Header -->
         
        <div class="relative z-10 flex justify-between items-center w-full">
          <div class="px-4 pt-4 flex flex-col items-center">
            <h1 class="font-bold ml-auto text-lg text-white">Waifu <span class="text-[#00A8FF]">Card</span></h1>
            <div class="border-b- mt-2 border-[#00A8FF] w-full mx-2"></div>
          </div>
          <div class="pt-4 flex items-center justify-end space-x-2">
            <button onclick="changeAmount({{data.id}}, -1)" class="fas fa-minus w-8 h-8" style="color: white;">
            </button>
            <button onclick="changeAmount({{data.id}}, 1)" class="fas fa-plus w-8 h-8" style="color: white;">
            </button>
            <button onclick="deleteCard({{data.id}})" class="fas fa-trash w-8 h-8" style="color: red;">
            </button>
          </div>
           
        </div>
        <!-- Card Body -->
        <div class="relative z-10 p-4">
          <!-- Waifu Name & Amount -->
          <div class="flex justify-between items-center mb-2">
            <h2 class="text-lg font-semibold text-[#00A8FF]">{{ data.name }}</h2>
            <div class="ml-2 text-white px-3 py-1 text-sm rounded-md bg-teal-950 hover:bg-teal-900">
              <h1>{{ data.amount }}</h1>
            </div>
          </div>
          <!-- Waifu Description -->
          <p class="text-white text-sm" style="overflow: hidden; text-overflow: ellipsis; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical;">{{ data.description }}</p>
          <!-- Waifu Stats -->
          <div class="mt-4">
            <h3 class="text-lg font-semibold text-[#00A8FF]">STATS</h3>
            <div class="flex flex-col">
              <div class="flex flex-col justify-center">
                <label for="strength" class="text-white text-sm">Strength</label>
                <div class="flex justify-between items-center">
                  <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                    <div class="bg-{% if data.strength <= 25 %}green-600{% elif data.strength <= 50 %}yellow-600{% elif data.strength <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.strength }}%;"></div>
                  </div>
                  <span class="ml-2 text-white">{{ data.strength }}</span>
                </div>
              </div>
              <div class="flex flex-col justify-center">
                <label for="speed" class="text-white text-sm">Speed</label>
                <div class="flex justify-between items-center">
                  <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                    <div class="bg-{% if data.speed <= 25 %}green-600{% elif data.speed <= 50 %}yellow-600{% elif data.speed <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.speed }}%;"></div>
                  </div>
                  <span class="ml-2 text-white">{{ data.speed }}</span>
                </div>
              </div>
              <div class="flex flex-col justify-center">
                <label for="potential" class="text-white text-sm">Potential</label>
                <div class="flex justify-between items-center">
                  <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                    <div class="bg-{% if data.potential <= 25 %}green-600{% elif data.potential <= 50 %}yellow-600{% elif data.potential <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.potential }}%;"></div>
                  </div>
                <span class="ml-2 text-white">{{ data.potential }}</span>
                </div>
              </div>
              <div class="flex flex-col justify-center">
                <label for="intelligence" class="text-white text-sm">Intelligence</label>
                <div class="flex justify-between items-center">
                  <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                    <div class="bg-{% if data.intelligence <= 25 %}green-600{% elif data.intelligence <= 50 %}yellow-600{% elif data.intelligence <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.intelligence }}%;"></div>
                  </div>
                  <span class="ml-2 text-white">{{ data.intelligence }}</span>
                </div>
              </div>
              <div class="flex flex-col justify-center">
                <label for="endurance" class="text-white text-sm">Endurance</label>
                <div class="flex justify-between items-center">
                  <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                    <div class="bg-{% if data.endurance <= 25 %}green-600{% elif data.endurance <= 50 %}yellow-600{% elif data.endurance <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.endurance }}%;"></div>
                  </div>
                  <span class="ml-2 text-white">{{ data.endurance }}</span>
                </div>
              </div>
            </div>
          </div>
          <!-- Waifu Physical Attributes -->
          <div class="mt-4 flex flex-col">
            <h3 class="text-lg font-semibold text-[#00A8FF]">Physical Attributes</h3>
            <div class="flex justify-between items-center text-white">
              <h1 class="text-sm">Height</h1>
              <div class=" px-2 py-1 bg-slate-900 rounded-md text-sm">{{ data.height }} cm</div>
            </div>
            <div class="flex justify-between items-center text-white space-y-3">
              <h1 class="text-sm">Weight</h1>
              <div class=" px-2 py-1 bg-slate-900 rounded-md text-sm">{{ data.weight }} kg</div>
            </div>
          </div>
        </div>
        <div id="card-rank-{{data.id}}" class="z-0  w-full absolute font-bold text-[#00A8FF] opacity-30 inset-0 flex items-center justify-center text-[24rem]">
          A
        </div>
        <script>
          function calculateRank(strength, speed, intelligence, potential, endurance) {
             // Menghitung nilai total stats
            var totalStats = (strength + speed + intelligence + potential + endurance) / 5;

            // Menentukan kisaran rank berdasarkan total stats
            if (totalStats >= 90) {
              return 'S';
            } else if (totalStats >= 80) {
              return 'A';
            } else if (totalStats >= 70) {
              return 'B';
            } else if (totalStats >= 60) {
              return 'C';
            } else if (totalStats >= 50) {
              return 'D';
            } else {
              return 'E';
            }
          }  
          var element = document.getElementById("card-rank-{{ data.id }}");
          var strength = {{ data.strength }};
          var speed = {{ data.speed }};
          var intelligence = {{ data.intelligence }};
          var potential = {{ data.potential }};
          var endurance = {{ data.endurance }};
          if(element){
            console.log('here')
            element.innerText = calculateRank(strength, speed, intelligence, potential, endurance)
          }
        </script>
      </div>
      {% endfor %}
    </div>
    {% endif %}
       
     
  </div>

  <script>

    const myElement = document.getElementById('loadingOverlay');


    window.addEventListener('load', function() {
      myElement.style.display = 'none';
    });
    function onLogout (){
      myElement.style.display = 'flex';
      setTimeout(function() {
        myElement.style.display = 'none';
      }, 5000);
    }
    function onClickAdd(){
      myElement.style.display = 'flex';
      setTimeout(function() {
      myElement.style.display = 'none';
    }, 5000);
    }
    function deleteCard(id){
      myElement.style.display = 'flex';
      const csrftoken = getCookie('csrftoken');
      const formData = new FormData();
      formData.append('waifu_card_id', id);
      fetch('/main/deleteCard/', {
      method: 'POST',
      headers: {
        'X-CSRFToken': csrftoken
      },
      body: formData
    })
    .then(response => {
      if (response.status === 200) {
        // Handle berhasil
        // myElement.style.display = 'none';
        console.log('Perubahan jumlah berhasil');
        console.log(response)
        window.location.href = '/main/';
      } else {
        // Handle kesalahan jika diperlukan
        //myElement.style.display = 'none';
        console.error('Terjadi kesalahan:', response.statusText);
        myElement.style.display = 'none';
      }
    })
    .catch(error => {
      //myElement.style.display = 'none';
      console.error('Terjadi kesalahan:', error);
      myElement.style.display = 'none';
    });
    }
    function changeAmount(id, quantity){
      myElement.style.display = 'flex';
      const csrftoken = getCookie('csrftoken');
      const formData = new FormData();
      formData.append('waifu_card_id', id);
      formData.append('quantity', quantity);
      fetch('/main/changeAmount/', {
      method: 'POST',
      headers: {
        'X-CSRFToken': csrftoken
      },
      body: formData
    })
    .then(response => {
      if (response.status === 200) {
        window.location.href = '/main/';
      } else {
        console.error('Terjadi kesalahan:', response.statusText);
        myElement.style.display = 'none';
      }
    })
    .catch(error => {
      console.error('Terjadi kesalahan:', error);
      myElement.style.display = 'none';
    });
    }

    function getCookie(name) {
    const value = `; ${document.cookie}`;
    const parts = value.split(`; ${name}=`);
    if (parts.length === 2) return parts.pop().split(';').shift();
  }
     
  </script>
  {% endblock content %}
```

TUGAS 4

deployment: https://waifu-collection.vercel.app/

1.
User Creation Form adalah formulir bawaan yang disediakan oleh Django dalam membuat instance dari User. User Creation Form secara default memiliki field username, password (password1), dan password confirmation (password2).  

Kelebihan:

a. UserCreationForm adalah formulir bawaan yang siap pakai untuk melakukan aktivitas registrasi user, sehingga kita tidak perlu menulis formulir pendaftaran pengguna dari awal.

b. UserCreationForm terintegrasi dengan baik dengan sistem otentikasi Django. Ini memungkinkan kita untuk dengan mudah menyimpan informasi pengguna yang terdaftar dalam database dan melakukan otentikasi dengan mereka.

c. Django UserCreationForm dilengkapi dengan validasi bawaan yang berfungsi untuk memeriksa data yang dimasukkan oleh pengguna dalam proses pendaftaran. Validasi ini dirancang untuk memastikan bahwa data yang diberikan oleh pengguna sesuai dengan aturan yang telah ditetapkan. Hal tersebut juga membuat kita setidaknya tidak memiliki kewajiban untuk membuat validasi manual begitu mendapatkan data dari Post Request.

d. Formulir ini secara otomatis menyinkronkan data yang dimasukkan oleh pengguna, meverifikasi data, dan membuat objek User dalam database.

Kekurangan:

a. UserCreationForm tidak memiliki validasi yang responsif di sisi klien, yang berarti pengguna harus menunggu hingga data dikirimkan ke server sebelum mereka mendapatkan umpan balik tentang apakah input mereka valid atau tidak. Hal ini tentu saja dapat mengurangi _user experience_ bagi klien, terutama pada aplikasi dan web yang memerlukan validasi real-time.

b.  Desain default dari UserCreationForm terlihat begitu sederhana dan bisa dikatakan buruk. Untuk memperbaiki desain tersebut, ujung-ujungnya nanti kita harus membuat kotak, label, dan elemen input secara manual yang kemudian dipadukan dengan kelas kelas CSS. Hal tersebut bisa dibilang tidak beda jauh dengan membuat form pendaftaran secara manual.

c.  UserCreationForm memiliki field bawaan yang terbatas, yaitu username, password1, dan password2. Jika kita memerlukan tambahan field maka kita perlu membuatnya secara manual dan secara terpisah mengambil field tambahan tersebut dari body request. Ada alternatif lain yaitu dengan membuat kelas form yang meng-_extends_ UserCreationForm.

d.  UserCreationForm sangat terkait erat dengan sistem otentikasi bawaan Django. Jika kita ingin menggunakan otentikasi yang berbeda atau khusus, maka UserCreationForm bukan pilihan yang tepat.

e.  Formulir ini menyediakan validasi bawaan dan perlindungan melalui csrf token, tetapi tidak termasuk fitur-fitur keamanan tambahan seperti CAPTCHA yang dapat membantu melindungi form dari serangan bot.


2. Dalam konteks Django, autentikasi adalah proses untuk memverifikasi identitas klien. Contohnya adalah dengan login, maka sistem mengetahui bahwa klien tersebut adalah pemilik akses yang sah atau tidak. Sementara itu, otorisasi adalah proses untuk mengontrol hak akses klien setelah klien berhasil diautentikasi. Dalam hal ini, contohnya adalah  kita sebagai user dapat memodifikasi objek yang kita buat, akan tetapi kita tidak diberikan izin untuk memodifikasi objek yang dibuat oleh orang lain. Hal tersebut berbeda lagi dengan admin, admin dapat memodifikasi semua benda yang dibuat oleh siapapun. Autentikasi dan otorisasi penting untuk dilakukan karena dapat melindungi integritas data, melindungi data sensitif, dan menghindari penyalahgunaan sistem.

3. Cookie adalah  data berukuran kecil yang berbentuk teks yang berisi informasi non-sensitif yang disimpan di sisi klien (misal web peramban). Cookie  di-generate oleh server dan digunakan untuk meningkatkan user-experience klien. Dengan kata lain, cookie digunakan untuk mempersonalisasi klien tersebut. Django menggunakan cookies untuk mengelola data sesi pengguna dengan cara menyimpan sesi tersebut di dalam cookie secara default. Hal tersebut dilakukan dengan menuliskan hal ini di dalam settings.py
`SESSION_ENGINE = "django.contrib.sessions.backends.cookie"`

4. Penggunaan cookies dalam pengembangan web tidak selalu aman secara default karena selalu ada risiko potensial yang perlu diwaspadai.

a. Resiko pencurian cookie

Pencurian cookie dapat memungkinkan penyerang untuk mengakses akun pengguna dengan mencuri sesi yang aktif. Hal tersebut mengakibatkan akses yang tidak sah ke data pribadi dan informasi sensitif. Pencurian cookie juga dapat mengancam privasi pengguna dengan memberikan penyerang akses ke riwayat penelusuran, preferensi, dan aktivitas online pengguna, yang dapat digunakan untuk hal-hal yang tidak sah. Salah satu metode untuk mencuri cookie adalah dengan menggunakan teknik XSS. Dalam teknik tersebut, penyerang memasukkan skrip berbahaya ke dalam halaman web yang dilihat oleh pengguna. Skrip ini dapat digunakan untuk mencuri cookie pengguna yang saat itu sedang digunakan untuk sesi web yang aktif.

b. Tracking dan Profiling

Penggunaan cookie oleh perusahaan periklanan dan analitik dapat mengumpulkan data perilaku pengguna secara luas untuk profil dan penargetan iklan. Ini bisa menjadi risiko privasi jika data tersebut digunakan tanpa izin atau disalahgunakan.

5.
a. Mengimplementasikan fungsi registrasi, login, dan logout

Kita perlu membuat fungsi-fungsi tersebut di dalam views.py. Untuk fungsi registrasi dan login kita perlu memikirkan jenis request yang masuk, apakah GET request atau POST request. Apabila yang masuk adalah GET request maka kita harus merender tampilan. Sementara jika yang masuk adalah POST request maka kita harus melakukan autentikasi dengan data yang dikirimkan melalui POST request tersebut. Sementara untuk fungsi logout, kita hanya perlu memikirkan cara kita meng-handle GET request yang masuk, yaitu dengan cara melakukan logout terhadap request.user.

### views.py
```
...
def register(request):
    form = UserCreationForm()

    if request.method == "POST":
        form = UserCreationForm(request.POST)
        print(form.is_valid())
        
        if form.is_valid():
            form.save()
            messages.success(request, 'Your account has been successfully created!')
            return redirect('main:login')
    context = {'form': form}
    return render(request, 'register.html', context)

def login_user(request):
    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            response = HttpResponseRedirect(reverse("main:home")) 
            response.set_cookie('last_login', str(datetime.datetime.now()))
            return response
        else:
            messages.info(request, 'Sorry, incorrect username or password. Please try again.')
    context = {}
    return render(request, 'login.html', context)

def logout_user(request):
    logout(request)
    response = HttpResponseRedirect(reverse('main:login'))
    response.delete_cookie('last_login')
    return response
...
```
Selanjutnya kita perlu mendaftarkan routing untuk mengakses fungsi-fungsi tersebut.
### urls.py
```
...
path('register/', register, name='register'), 
path('login/', login_user, name='login'),
path('logout/', logout_user, name="logout"),
...
```
Kemudian kita buat template yang bersesuaian di folder templates yang berada di directory main
### register.html
```
{% extends 'base.html' %}
{% block meta %}
    <title>Register</title>
    
{% endblock meta %}
{% block content %}
<div id="loadingOverlay" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50">
   
    <div  role="status" class="bg-white bg-opacity-50 rounded-lg p-4 shadow-lg flex justify-center items-center">
        <svg aria-hidden="true" class="w-10 h-10  text-gray-200 animate-spin dark:text-gray-600 fill-blue-600" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z" fill="currentColor"/>
            <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z" fill="currentFill"/>
        </svg>
    </div>
</div>
<div class=" hidden md:flex fixed right-0 top-0 h-screen w-3/4 bg-blue-700 -z-20" style="clip-path: polygon(100% 0%, 100% 100%, 0% 100%, 80% 0%);">
</div>

<div class=" min-h-screen overflow-y-auto flex flex-col justify-center items-center w-screen">
    <div class="mb-4 flex font-bold w-full text-white lg:text-4xl md:text-2xl text-xl">
        <h1 class=" mx-auto">Buat Akun <span class="text-[#00A8FF]">Waifu Baru</span> </h1>
    </div>
    <form  class="flex flex-col min-h-[28rem] bg-slate-950 px-4 py-2 rounded-md text-white max-w-[95%] min-w-[20rem] md:w-[28rem] w-[24rem]" autocomplete="off" method="post">
        {% csrf_token %}
        <div class="mb-4">
            <label for="{{ form.username.id_for_label }}" class="block text-white text-sm  mb-2">Username</label>
            <input type="text" name="username"  class=" bg-slate-800 focus:border  text-white  text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" placeholder="Masukkan nama kamu" id="{{ form.username.id_for_label }}">
            <p class="mt-2 text-[#00A8FF] text-xs text-justify">Required. 150 characters or fewer. Letters, digits and @/./+/-/_ only.</p>
        </div>
        <div class="mb-4">
            <label for="{{ form.password1.id_for_label }}" class="block text-white text-sm  mb-2">Password</label>
            <input type="password" name="password1" class="bg-slate-800 focus:border  text-white  text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" placeholder="Buat password" id="{{ form.password1.id_for_label }}">
            <p  class="mt-2 text-[#00A8FF] text-xs text-justify">Your password can`t be too similar to your other personal information.
                Your password must contain at least 8 characters.
                Your password can`t be a commonly used password.
                Your password can`t be entirely numeric.</p>
        </div>
        <div class="mb-4">
            <label for="{{ form.password2.id_for_label }}" class="block text-white text-sm  mb-2">Confirm Password</label>
            <input type="password" name="password2" class="bg-slate-800 focus:border  text-white  text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"placeholder="Ulangi password" id="{{ form.password2.id_for_label }}">
            <p class="mt-2 text-[#00A8FF] text-xs text-justify">Enter the same password as before, for verification.</p>
        </div>
        <div class="mb-4">
            <h1 class="block text-white text-sm  mb-2">Sudah punya akun? <span><a href="{% url 'main:login' %}" class="font-bold text-[#00A8FF]">Login</a></span></h1>
        </div>  
        <div class="mb-4 mt-auto">
            <hr class=" border-2 rounded-md border-[#00A8FF]">
        </div>
        <div class="mb-2 w-full   text-sm flex">
            <button onclick="onSubmit()" class="ml-auto px-4 py-2 bg-[#00A8FF] text-black hover:text-white hover:bg-blue-900 rounded-sm"type="submit">Buat Akun</button>
        </div>
        
    </form>
    
</div>
<script>
const myElement = document.getElementById('loadingOverlay');
window.addEventListener('load', function() {
    myElement.style.display = 'none';
});
function onSubmit (){
myElement.style.display = 'flex';
setTimeout(function() {
    myElement.style.display = 'none';
}, 5000);
}
</script>
{% endblock content %}
```
### login.html
```
{% extends 'base.html' %}
{% block meta %}
    <title>Masuk ke Akun Waifu</title>
    
{% endblock meta %}
{% block content %}
<div id="loadingOverlay" class="fixed inset-0 flex items-center justify-center z-50 bg-black bg-opacity-50">
   
    <div  role="status" class="bg-white bg-opacity-50 rounded-lg p-4 shadow-lg flex justify-center items-center">
        <svg aria-hidden="true" class="w-10 h-10  text-gray-200 animate-spin dark:text-gray-600 fill-blue-600" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z" fill="currentColor"/>
            <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z" fill="currentFill"/>
        </svg>
    </div>
</div>
<div class=" hidden md:flex fixed right-0 top-0 h-screen w-3/4 bg-blue-700 -z-20" style="clip-path: polygon(100% 0%, 100% 100%, 0% 100%, 80% 0%);">
</div>

<div class=" min-h-screen overflow-y-auto flex flex-col justify-center items-center w-screen">
    <div class="mb-4 flex font-bold w-full text-white lg:text-4xl md:text-2xl text-xl">
        <h1 class=" mx-auto">Login Akun <span class="text-[#00A8FF]">Waifu Kamu</span> </h1>
    </div>
    <form  class="flex flex-col min-h-[28rem] bg-slate-950 px-4 py-2 rounded-md text-white max-w-[95%] min-w-[18rem] md:w-[28rem] w-[24rem]" autocomplete="off" method="post">
        {% csrf_token %}
        <div class="mb-4">
            <label for="username" class="block text-white text-sm  mb-2">Username</label>
            <input autocomplete="off" required type="text" name="username"  class=" bg-slate-800 focus:border  text-white  text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" placeholder="Masukkan nama kamu" id="username">
        </div>
        <div class="mb-4">
            <label for="password" class="block text-white text-sm  mb-2">Password</label>
            <input autocomplete="off" required type="password" name="password" class="bg-slate-800 focus:border  text-white  text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" placeholder="Buat password" id="password">
        </div>
        <div class="mb-4">
            <h1 class="block text-white text-sm  mb-2">Belum punya akun? <span><a href="{% url 'main:register' %}" class="font-bold text-[#00A8FF]">Register</a></span></h1>
        </div>  
        <div class="mb-4 mt-auto">
            <hr class=" border-2 rounded-md border-[#00A8FF]">
        </div>
        <div class="mb-2 w-full   text-sm flex">
            <button onclick="onSubmit()" class="ml-auto px-4 py-2 bg-[#00A8FF] text-black hover:text-white hover:bg-blue-900 rounded-sm"type="submit">Masuk</button>
        </div>
        
    </form>
</div>
<script>
const myElement = document.getElementById('loadingOverlay');


window.addEventListener('load', function() {
    myElement.style.display = 'none';
});
function onSubmit (){
myElement.style.display = 'flex';
setTimeout(function() {
    myElement.style.display = 'none';
}, 5000);
}
</script>
{% endblock content %}
```

b. Kemudian kita registrasikan dua user dan kemudian untuk masing masing user, kita tambahkan tiga objek kartu.

c. Untuk menghubungkan User dengan Item maka kita perlu memperbarui field model Item dengan menambahkan `user = models.ForeignKey(User, on_delete=models.CASCADE)`
### models.py
```
...
class Item(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    name= models.CharField(max_length=255)
    amount= models.IntegerField(validators=[MinValueValidator(0)])
    description=models.TextField()
    strength = models.PositiveIntegerField()
    speed = models.PositiveIntegerField() 
    potential = models.PositiveIntegerField() 
    intelligence = models.PositiveIntegerField() 
    endurance = models.PositiveIntegerField() 
    height = models.DecimalField(max_digits=5, decimal_places=2)
    weight = models.DecimalField(max_digits=5, decimal_places=2)
...
```
Selanjutnya kita perlu memfilter kartu dengan user yang sesuai dengan kode `waifus = Item.objects.filter(user=request.user)` pada fungsi home.
### views.py
```
...
@login_required(login_url='/main/login')
def home(request):
    waifus = Item.objects.filter(user=request.user)
    user = request.user
    card_total = 0
    last_login = request.COOKIES['last_login']
    if last_login is None:
        last_login = "Belum ada data"
    for waifu in waifus:
        card_total += waifu.amount
    return render(request, "home.html", {'waifus': waifus, 'username': user.username, 'total':card_total, 'last_login': last_login,})

...
```

d. Untuk menampilkan detail informasi pengguna yang sedang logged in seperti username dan menerapkan cookies seperti last login pada halaman utama aplikasi, kita perlu menambahkan cookie.
Hal tersebut dapat kita lakukan ketika user berhasil diautentikasi saat login. Tambahkan kode ini `response.set_cookie('last_login', str(datetime.datetime.now()))` pada fungsi login_user.
### views.py
```
...
def login_user(request):
    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            response = HttpResponseRedirect(reverse("main:home")) 
            response.set_cookie('last_login', str(datetime.datetime.now()))
            return response
        else:
            messages.info(request, 'Sorry, incorrect username or password. Please try again.')
    context = {}
    return render(request, 'login.html', context)
...
```
Selanjutnya, pada halaman utama, kita perlu mengambil cookie tersebut dengan menambahkan kode `last_login = request.COOKIES.get('last_login', 'Tidak ada data')` pada fungsi home
### views.py
```
...
@login_required(login_url='/main/login')
def home(request):
    waifus = Item.objects.filter(user=request.user)
    user = request.user
    card_total = 0
    last_login = request.COOKIES.get('last_login', 'Tidak ada data') #mengambil cookie
    for waifu in waifus:
        card_total += waifu.amount
    return render(request, "home.html", {'waifus': waifus, 'username': user.username, 'total':card_total, 'last_login': last_login,})
...
```
Kemudian menghapus cookie tersebut ketika kita logout dengan menambahkan kode `response.delete_cookie('last_login')` pada fungsi logout_user
### views.py
```
...
def logout_user(request):
    logout(request)
    response = HttpResponseRedirect(reverse('main:login'))
    response.delete_cookie('last_login')
    return response
...
```

TUGAS 3

deployment: https://waifu-collection.vercel.app/

1.
Ketika menggunakan Form Post atau post request, data yang dikirimkan ke server dibungkus dalam body milik request tersebut sehingga data tidak terlihat oleh pihak ketiga. Sementara itu, pada Form Get atau get request, data yang dikirimkan ke server menjadi bagian Head atau kepala dari request tersebut dan data tersebut terlihat di URL yang mana dapat dilihat oleh pihak ketiga. Meskipun keduanya dapat dilakukan untuk hal yang sama, akan tetapi berdasarkan konvensi keduanya memiliki peruntukan yang berbeda. Form Post digunakan untuk mengirim data yang tujuannya untuk memodifikasi database sementara Form Get hanya untuk mendapatkan data yang sifatnya tidak sensitif dan tidak pula mengubah status. Form get cenderung lebih cepat daripada form post karena tidak memiliki overhead alias datanya terpusat di bagian head saja. Selain itu, Get Request dapat di-cache oleh browser sementara  Post Request tidak dapat dicache oleh browser.

2.
Perbedaan utama diantara ketiganya sebagai berikut:
XML
XML berbentuk markup language dengan tag yang dapat kita buat sendiri. XML menerapkan struktur atau disebut juga struktur hierarkis dalam mengorganisir datanya. XML tidak memiliki tipe data default sehingga mudah diuraikan dan fleksibel untuk dikonversi ke bentuk objek lainnya.

JSON
JSON merepresentasikan data dalam bentuk objek javascript yang mirip seperti map atau dicitionary. JSON mengorganisir datanya dengan menggunakan value-key pair atau dengan kata lain menggunakan struktur map. Tidak hanya itu JSON juga memiliki ukuran file yang lebih kecil dari format data lain sehingga hal ini menyebabkan JSON memiliki performa yang lebih baik daripada XML. Meskipun tidak se-fleksibel XML tetapi JSON sendiri sudah cukup mendukung banyak struktur data maupun objek.

HTML
Html sebenarnya merupakan markup language yang lebih diperuntukkan untuk membuat tampilan dan konten dari suatu website daripada menjadi format pengiriman data. Tag pada html juga sudah default dari sananya dan kita tidak bisa membuat custom tag sendiri.

3.
JSON memiliki Sintaks yang Mudah Dibaca
JSON memiliki sintaknya yang ringkas dan mudah dibaca oleh manusia. JSON menggunakan format objek dengan pasangan "kunci-nilai" yang intuitif dan mudah dinterpretasikan oleh manusia.

Mudah Diproses
JSON mudah diproses oleh komputer. Kebanyakan bahasa pemrograman modern memiliki dukungan yang baik untuk parsing dan menghasilkan data dalam format JSON. Ini membuatnya mudah untuk mengubah data dalam format JSON menjadi objek atau struktur data yang dapat digunakan oleh aplikasi.

Mendukung Tipe Data yang Umum
JSON mendukung tipe data umum seperti string, angka, boolean, objek, dan array. Ini mencakup sebagian besar tipe data yang diperlukan dalam pertukaran data.

Kompabilitas Tinggi
JSON mendukung berbagai bahasa pemrograman. Hampir semua bahasa pemrograman modern memiliki dukungan untuk mengurai (parsing) dan menghasilkan data dalam format JSON. Ini membuatnya sangat cocok untuk berkomunikasi antara berbagai aplikasi dan sistem yang ditulis dalam bahasa yang berbeda.

4.
Langkah-langkahnya sebagai berikut:

a. Membuat base.html

```plaintext
{% load static %}
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta
            name="viewport"
            content="width=device-width, initial-scale=1.0"
        />
        <script src="https://cdn.tailwindcss.com"></script>
        {% block meta %}
        {% endblock meta %}
    </head>


    <body class="bg-slate-900">
        {% block content %}
        {% endblock content %}
    </body>
</html>
```
base.html ini diletakkan di folder templates yang berada di root directory.

b. Tambahkan fungsi create_card di views.py pada directory aplikasi main
Kode fungsi tersebut adalah sebagai berikut
```
def create_card(request):
    if request.method == 'POST':
        name = request.POST.get('name')
        amount = request.POST.get('amount')
        description = request.POST.get('description')
        strength = request.POST.get('strength')
        speed = request.POST.get('speed')
        potential = request.POST.get('potential')
        intelligence = request.POST.get('intelligence')
        endurance = request.POST.get('endurance')
        height = request.POST.get('height')
        weight = request.POST.get('weight')
        item = Item(
            name=name,
            amount=amount,
            description=description,
            strength=strength,
            speed=speed,
            potential=potential,
            intelligence=intelligence,
            endurance=endurance,
            height=height,
            weight=weight,
        )
        item.save()
        return redirect('main:home')


    return render(request, "addCard.html",{})
```
Fungsi tersebut memiliki parameter request yang berasal dari routing permintaan client di urls.py yang berada di tingkat project dan app (main). Fungsi tersebut menangani permintaan GET dan POST. Apabila permintaan berupa POST maka kita akan mengambil nilai-nilai yang tersimpan di body request tersebut dan kemudian menjadikannya sebagai instance dari model Item untuk selanjutnya disimpan ke db (database). Sementara itu, apabila permintaan berupa GET maka kita akan me-render template addCard.html

c. Membuat fungsi untuk menampilkan data dalam HTML, XML, JSON, XML by ID, dan JSON by ID
Kodenya adalah sebagai berikut
```
from django.shortcuts import render, redirect
from .models import Item
from django.http import HttpResponse
from django.core import serializers


def create_card(request):
    if request.method == 'POST':
        name = request.POST.get('name')
        amount = request.POST.get('amount')
        description = request.POST.get('description')
        strength = request.POST.get('strength')
        speed = request.POST.get('speed')
        potential = request.POST.get('potential')
        intelligence = request.POST.get('intelligence')
        endurance = request.POST.get('endurance')
        height = request.POST.get('height')
        weight = request.POST.get('weight')
        item = Item(
            name=name,
            amount=amount,
            description=description,
            strength=strength,
            speed=speed,
            potential=potential,
            intelligence=intelligence,
            endurance=endurance,
            height=height,
            weight=weight,
        )
        item.save()
        return redirect('main:home')


    return render(request, "addCard.html",{})


# Menambahkan fungsi untuk melihat kartu yang telah ditambahkan

def home(request):
    waifus = Item.objects.all()
    card_total = 0
    for waifu in waifus:
        card_total += waifu.amount
    return render(request, "home.html", {'waifus': waifus, 'total':card_total})

def show_xml_by_id(request, id):
    data = Item.objects.filter(pk=id)
    return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")
def show_json_by_id(request, id):
    data = Item.objects.filter(pk=id)
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")
def show_json(request):
    data = Item.objects.all()
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")
def show_xml(request):
    data = Item.objects.all()
    return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")
```

d. Mengupdate routing pada tingkat app main
Kodenya adalah sebagai berikut
```
from django.urls import path
from .views import home, create_card, show_json_by_id, show_xml_by_id, show_json, show_xml
app_name = 'main'
urlpatterns = [
    path('', home, name='home'), 
    path('addCard/', create_card, name='addCard'),
    path('json/', show_json, name='show_json'), 
    path('xml/', show_xml, name='show_xml'),
    path('xml/<int:id>/', show_xml_by_id, name='show_xml_by_id'),
    path('json/<int:id>/', show_json_by_id, name='show_json_by_id'),
  ]
```
Routing ini dilakukan di urls.py pada tingkat direktori app main. Hal tersebut agar request yang masuk dapat dimapping ke fungsi views yang sesuai.

e. Memodifikasi main.html
Buat modifikasi pada template home.html dengan melakukan inheritance terhadap template base.html. Selain itu kita juga perlu menambahkan sebuah button di ujung kanan atas untuk mengarahkan kita ke halaman form membuat kartu. Kode untuk home.html adalah sebagai berikut
```
{% extends 'base.html' %}


    {% block meta %}
    <title>Waifu Card Collection</title>
    
    {% endblock meta %}
    
    {% block content %}
    <div class="w-screen min-h-screen flex flex-col">
        <div class=" hidden md:flex fixed right-0 top-0 h-screen w-3/4 bg-blue-700 -z-20" style="clip-path: polygon(100% 0%, 100% 100%, 0% 100%, 80% 0%);">
        </div>
        <a href="{% url 'main:addCard' %}" class="fixed top-2 right-2 text-white px-4 py-2 text-base rounded-md bg-slate-950 hover:bg-teal-900">
            <h1>Tambah Kartu</h1>
        </a>
        <div class="flex flex-col w-full text-base p-4 text-white font-bold ">
            <div class="  p-4 rounded-md bg-opacity-30 text-base">
                <h1>Nama Aplikasi: <span class="text-[#00A8FF]">Waifu Card Collection</span></h1>
            <h1>Nama: <span class="text-[#00A8FF]">Isa Citra Buana</span></h1>
            <h1>NPM: <span class="text-[#00A8FF]">2206081465</span></h1>
            <h1>Kelas: <span class="text-[#00A8FF]">PBP D</span></h1>
            </div>
            <div class=" mx-auto mt-4 text-white font-bold text-base ">
                <h1>Terdapat <span class="text-[#00A8FF]">{{total}} kartu waifu </span></h1>
            </div>


        </div>
        
        {% if waifus|length == 0 %}
            <div class="flex w-full justify-center text-sm md:text-base lg:text-lg text-white font-bold h-full items-center">
                <h1> Belum ada waifu. Silahkan menambahkan</h1>
            </div>
        {% else %}
            <div class="mb-4  mx-auto gap-4 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 justify-center ">
            {% for data in waifus %}
            <div class="max-w-[24rem] px-4 mx-auto bg-slate-950 rounded-lg shadow-lg mt-2 overflow-hidden">
                <!-- Card Header -->
                <div class="px-4 pt-4 flex flex-col items-center">
                    <h1 class="font-bold ml-auto text-lg text-white">Waifu <span class="text-[#00A8FF]">Card</span></h1>
                    <div class="border-b-2 mt-2 border-[#00A8FF] w-full mx-2"></div>
                </div>
                <!-- Card Body -->
                <div class="p-4">
                    <!-- Waifu Name & Amount -->
                    <div class="flex justify-between items-center mb-2">
                        <h2 class="text-lg font-semibold text-[#00A8FF]">{{ data.name }}</h2>
                        <div class="ml-2 text-white px-3 py-1 text-sm rounded-md bg-teal-950 hover:bg-teal-900">
                            <h1>{{ data.amount }}</h1>
                        </div>
                    </div>
                    <!-- Waifu Description -->
                    <p class="text-white text-sm" style="overflow: hidden; text-overflow: ellipsis; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical;">{{ data.description }}</p>
                    <!-- Waifu Stats -->
                    <div class="mt-4">
                        <h3 class="text-lg font-semibold text-[#00A8FF]">STATS</h3>
                        <div class="flex flex-col">
                            <div class="flex flex-col justify-center">
                                <label for="strength" class="text-white text-sm">Strength</label>
                                <div class="flex justify-between items-center">
                                    <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                                        <div class="bg-{% if data.strength <= 25 %}green-600{% elif data.strength <= 50 %}yellow-600{% elif data.strength <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.strength }}%;"></div>
                                    </div>
                                    <span class="ml-2 text-white">{{ data.strength }}</span>
                                </div>
                            </div>
                            <div class="flex flex-col justify-center">
                                <label for="speed" class="text-white text-sm">Speed</label>
                                <div class="flex justify-between items-center">
                                    <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                                        <div class="bg-{% if data.speed <= 25 %}green-600{% elif data.speed <= 50 %}yellow-600{% elif data.speed <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.speed }}%;"></div>
                                    </div>
                                    <span class="ml-2 text-white">{{ data.speed }}</span>
                                </div>
                            </div>
                            <div class="flex flex-col justify-center">
                                <label for="potential" class="text-white text-sm">Potential</label>
                                <div class="flex justify-between items-center">
                                    <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                                        <div class="bg-{% if data.potential <= 25 %}green-600{% elif data.potential <= 50 %}yellow-600{% elif data.potential <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.potential }}%;"></div>
                                    </div>
                                <span class="ml-2 text-white">{{ data.potential }}</span>
                                </div>
                            </div>
                            <div class="flex flex-col justify-center">
                                <label for="intelligence" class="text-white text-sm">Intelligence</label>
                                <div class="flex justify-between items-center">
                                    <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                                        <div class="bg-{% if data.intelligence <= 25 %}green-600{% elif data.intelligence <= 50 %}yellow-600{% elif data.intelligence <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.intelligence }}%;"></div>
                                    </div>
                                    <span class="ml-2 text-white">{{ data.intelligence }}</span>
                                </div>
                            </div>
                            <div class="flex flex-col justify-center">
                                <label for="endurance" class="text-white text-sm">Endurance</label>
                                <div class="flex justify-between items-center">
                                    <div class="bg-white rounded-full h-[0.5rem] w-[90%]">
                                        <div class="bg-{% if data.endurance <= 25 %}green-600{% elif data.endurance <= 50 %}yellow-600{% elif data.endurance <= 75 %}orange-600{% else %}red-600{% endif %} h-full rounded-full" style="width: {{ data.endurance }}%;"></div>
                                    </div>
                                    <span class="ml-2 text-white">{{ data.endurance }}</span>
                                </div>
                            </div>
                        </div>
                    </div>
                    <!-- Waifu Physical Attributes -->
                    <div class="mt-4 flex flex-col">
                        <h3 class="text-lg font-semibold text-[#00A8FF]">Physical Attributes</h3>
                        <div class="flex justify-between items-center text-white">
                            <h1 class="text-sm">Height</h1>
                            <div class=" px-2 py-1 bg-slate-900 rounded-md text-sm">{{ data.height }} cm</div>
                        </div>
                        <div class="flex justify-between items-center text-white space-y-3">
                            <h1 class="text-sm">Weight</h1>
                            <div class=" px-2 py-1 bg-slate-900 rounded-md text-sm">{{ data.weight }} kg</div>
                        </div>
                    </div>
                </div>
            </div>
            {% endfor %}
        </div>
        {% endif %}
    </div>
    {% endblock content %}
```

f. Menambahkan addCard.html pada folder templates di tingkat direktori app main
Buat template addCard.html dengan melakukan inheritance terhadap base.html . Selanjutnya tambahkan tag form dengan atribut method yaitu post dan atribut action string kosong. Hal ini bertujuan agar form tersebut dikirimkan ke url yang sedang kita buka saat ini yaitu ." .../addCard ". Selanjutnya tambahkan {% csrf_token %} di dalam tag form tersebut. Pastikan kita harus membuat semua input yang dibutuhkan beserta atribut type yang sesuai. Selain itu kita juga harus memastikan atribut name sesuai dengan nama field pada model yang sedang kita tuju, dalam hal ini model Item. Terakhir tambahkan input bertipe submit agar ketika ditekan maka form dapat terkirim. Kodenya adalah sebagai berikut
```
{% extends 'base.html' %}

{% block meta %}
<title>Tambah Kartu</title>
{% endblock meta %}

{% block content %}
<div class=" hidden md:flex fixed right-0 top-0 h-screen w-3/4 bg-blue-700 -z-20" style="clip-path: polygon(100% 0%, 100% 100%, 0% 100%, 80% 0%);">
</div>
<div class="hidden fixed md:flex justify-end items-end w-screen h-screen -z-10 ">
    <img class=" w-96 h-auto"src="https://firebasestorage.googleapis.com/v0/b/isa-citra-1691878861005.appspot.com/o/marin-svg.svg?alt=media&token=4260c0db-77af-4631-b748-c1d562032baa" alt="">
</div>
<div class=" w-screen  min-h-screen flex lg:-ml-8 justify-center lg:justify-center md:justify-start items-center text-white">
    <div class= "flex flex-col items-center">
        <h1 class="mt-6 text-white text-4xl font-bold font-sans"> Tambah <span class="text-[#00A8FF]">Kartu Waifu</span></h1>
        <div class=" mt-4 md:mt-8 bg-slate-950 px-4 max-w-[95%] mx-2 md:min-w-[36rem] py-2 rounded-md">
            <form method="POST" action="">
                {% csrf_token %}
               
               <div class=" grid grid-cols-4 gap-4">
                <div class=" flex-col flex md:col-span-2 col-span-3">
                    <label for="name" class=" text-white mb-2 text-sm">Nama Waifu</label>
                    <input for="name" name="name" id="name" class="bg-slate-800 focus:border  text-white  text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" type="text" placeholder="Nama waifu idamanmu" required>
                </div>
                <div class="mb-2 md:col-span-2 col-span-1">
                    <label for="amount" class="block text-white text-sm mb-2">Amount</label>
                    <input
                    required
                        type="number"
                        id="amount"
                        name="amount"
                        min="1"
                        max="100"
                        step="1"
                        placeholder="Jumlah"
                        class="bg-slate-800 focus:border  text-white  text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                    >
                </div>
               </div>
                <div class=" grid-cols-2 md:grid gap-4">


                    <div class=" flex flex-col">
                        <label class="mt-2  mb-2 text-sm" for="strength">Strength</label>
                        <div class=" flex justify-between">
                            <input
                        required
                        class =" w-[90%]"
                        type="range"
                        id="strength"
                        name="strength"
                        min="1"
                        max="100"
                        step="1"
                        value="50"
                        oninput="updateOutput(this.value, 'strength-value'); "
                        >
                        <output for="strength" id="strength-value">50</output>
                        </div>
                    </div>


                    <div class=" flex flex-col">
                        <label class="mt-2  mb-2 text-sm" for="speed">Speed</label>
                        <div class=" flex justify-between">
                            <input
                        required
                        class =" w-[90%]"
                        type="range"
                        id="speed"
                        name="speed"
                        min="1"
                        max="100"
                        step="1"
                        value="50"
                        oninput="updateOutput(this.value, 'speed-value'); "
                        >
                        <output for="speed" id="speed-value">50</output>
                        </div>
                    </div>


                    <div class=" flex flex-col">
                        <label class="mt-2  mb-2 text-sm" for="intelligence">Intelligence</label>
                        <div class=" flex justify-between">
                            <input
                        required
                        class =" w-[90%]"
                        type="range"
                        id="intelligence"
                        name="intelligence"
                        min="1"
                        max="100"
                        step="1"
                        value="50"
                        oninput="updateOutput(this.value, 'intelligence-value')"
                        >
                        <output for="intelligence" id="intelligence-value">50</output>
                        </div>
                    </div>


                    <div class=" flex flex-col">
                        <label class="mt-2  mb-2 text-sm" for="potential">Potential</label>
                        <div class=" flex justify-between">
                            <input
                        required
                        class =" w-[90%]"
                        type="range"
                        id="potential"
                        name="potential"
                        min="1"
                        max="100"
                        step="1"
                        value="50"
                        oninput="updateOutput(this.value, 'potential-value');"
                        >
                        <output for="potential" id="potential-value">50</output>
                        </div>
                    </div>
                    <div class=" flex flex-col">
                        <label class="mt-2  mb-2 text-sm" for="endurance">Endurance</label>
                        <div class=" flex justify-between">
                            <input
                        required
                        class =" w-[90%]"
                        type="range"
                        id="endurance"
                        name="endurance"
                        min="1"
                        max="100"
                        step="1"
                        value="50"
                        oninput="updateOutput(this.value, 'endurance-value');"
                        >
                        <output for="endurance" id="endurance-value">50</output>
                        </div>
                    </div>
                   
                </div>
                <div class="flex flex-col">
                    <label for="description" class=" text-white mb-2 mt-2 text-sm">Deskripsi</label>
                    <textarea required id="description" for="description"name="description" class="bg-slate-800 focus:border  text-white  text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" type="text" placeholder="Deskripsi tentang waifumu"></textarea>
                </div>
                <div class=" grid grid-cols-2 gap-4 mt-2">
                    <div class="flex flex-col">
                        <label for="weight" class="block text-white text-sm mb-2">Weight (kg)</label>
                    <input
                        required
                        type="number"
                        id="weight"
                        name="weight"
                        min="1"
                        max="100"
                        step="0.5"
                        placeholder="Berat Waifu-mu"
                        class="bg-slate-800 focus:border  text-white  text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                    >
                    </div>
                    <div class="flex flex-col">
                        <label for="amount" class="block text-white text-sm mb-2">Height (cm)</label>
                    <input
                        required
                        type="number"
                        id="height"
                        name="height"
                        min="1"
                        max="200"
                        step="0.5"
                        placeholder="Tinggi waifu-mu"
                        class="bg-slate-800 focus:border  text-white  text-sm rounded-xs focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5"
                    >
                    </div>
                </div>
                <div class="flex mt-4">
                    <input type="submit" value="Tambah Kartu" class="ml-auto px-4 py-2 text-sm rounded-md bg-slate-900 hover:bg-slate-800">
                </div>
            </form>
        </div>
    </div>
</div>


<script>
    function updateOutput(value, elementId) {
        // Mengambil elemen output
        var outputElement = document.getElementById(elementId);
        
        // Mengubah teks pada elemen output sesuai dengan nilai input
        outputElement.textContent = value;
        
    }


</script>
{% endblock content %}
```
5.
Menampilkan screenshot postman:
a. Get request dalam bentuk html
![Gambar 1](html-img/vercel-get-main-1.png)
![Gambar 2](html-img/vercel-get-main-2.png)
![Gambar 3](html-img/vercel-get-main-3.png)
![Gambar 4](html-img/vercel-get-main-4.png)
![Gambar 5](html-img/vercel-get-main-5.png)
![Gambar 6](html-img/vercel-get-main-6.png)
![Gambar 7](html-img/vercel-get-main-7.png)
![Gambar 8](html-img/vercel-get-main-8.png)
![Gambar 9](html-img/vercel-get-main-9.png)
![Gambar 10](html-img/vercel-get-main-10.png)
![Gambar 11](html-img/vercel-get-main-11.png)
![Gambar 12](html-img/vercel-get-main-12.png)

b. Get request dalam bentuk json
![Gambar 1](json-img/vercel-get-json-1.png)
![Gambar 2](json-img/vercel-get-json-2.png)
![Gambar 3](json-img/vercel-get-json-3.png)
c. Get request dalam bentuk xml
![Gambar 1](xml-img/vercel-get-xml-1.png)
![Gambar 2](xml-img/vercel-get-xml-2.png)
d. Get request dalam json/:id
![Gambar 1](json-id-img/vercel-get-json-id-1.png)
![Gambar 2](json-id-img/vercel-get-json-id-2.png)
![Gambar 3](json-id-img/vercel-get-json-id-3.png)
e. Get request dalam xml/:id
![Gambar 1](xml-id-img/vercel-get-xml-id-1.png)
![Gambar 2](xml-id-img/vercel-get-xml-id-2.png)
![Gambar 3](xml-id-img/vercel-get-xml-id-3.png)

-----------------------------------------------------------------------------------------------------
TUGAS 2
https://waifu-card-collection.adaptable.app/

Nama: Isa Citra Buana
NPM: 2206081465


1. 
A.	Untuk membuat sebuah proyek Django yang baru. Kita bisa memulai baik dengan menggunakan virtual environment ataupun tidak menggunakan virtual environment. Apabila kita menggunakan virtual environment, maka step yang perlu kita lakukan adalah sebagai berikut:

a.	Buat virtual environment python. Apabila belum menginstal virtual environment, maka bisa menginstallnya terlebih dahulu dengan menuliskan “pip install virtualenv” di terminal device Anda. Kemudian tulis “python -m virtualenv (nama virtualenv yang ingin dibuat)” di terminal device Anda. Dalam hal ini nama virtualenv saya adalah sepuhvirtual.
b.	Setelah itu, pada direktori yang sama, Anda perlu mengaktifkan virtualenv tersebut dengan menuliskan “(nama virtualenv yang tadi Anda buat)\Scripts\activate”, berarti saya perlu melakukan “sepuhvirtual\Scripts\activate”.
c.	Kemudian install django dengan menuliskan “pip install django”.
d.	Buat projek django dengan menuliskan “django-admin startproject (nama project Anda)”. Dalam hal ini projek yang saya buat adalah WaifuCollection.

B.	Untuk membuat app pada proyek Django tersebut caranya adalah sebagai berikut:

a.	Pindah dulu ke directory projek tersebut. Dalam hal ini dengan mengasumsikan Anda berada pada directory yang sama sebelumnya, maka Anda perlu menuliskan “cd (nama projek anda)”, dalam hal ini saya berarti menuliskan “cd WaifuCollection”.
b.	Kemudian, buat sebuah app di projek tersebut dengan menuliskan “django-admin startapp (nama app Anda)”. Dalam hal ini, saya memilih menggunakan nama aplikasi saya adalah main. Kemudian buka folder projek Anda tersebut di VSCode Anda.
C.	Untuk melakukan routing pada aplikasi main tersebut agar dapat diakses di project Django, caranya adalah sebagai berikut:

a.	Navigasi ke settings.py pada directory projek, dalam hal ini directory tersebut WaifuCollection yang berada di dalam root projek WaifuCollection. 
b.	Pada settings.py, daftarkan aplikasi Anda, dalam hal ini aplikasi saya adalah main. Caranya adalah dengan menambahkan “main” pada  INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
   'django.contrib.sessions',
   'django.contrib.messages',
   'django.contrib.staticfiles',
   'main' ]
c.	Kemudian, konfigurasikan aplikasi main pada urls.py di tingkat proyek. Caranya adalah dengan menambahkan  path('/', include('main.urls'))  pada 
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('main.urls'))
]
Tujuan melakukan hal tersebut adalah untuk menetapkan  rute dasar untuk aplikasi main.

D.	Kemudian, kita perlu membuat model Item (terserah Anda memilih membuat model apa). Model bisa diibaratkan sebagai representasi Python dari tabel dalam basis data yang mendefinisikan struktur data dan aturan yang diterapkan pada data dalam aplikasi web Django. Dalam hal ini untuk membuatnya, Anda perlu navigasi ke models.py yang berada di directory aplikasi yang anda pilih, dalam hal ini saya memilih aplikasi main. Setelah itu, anda bisa menambahkan kelas model Item yang melakukan inheritance terhadap kelas models.model. Contohnya adalah seperti ini:

class Item(models.Model):
    name= models.CharField(max_length=255)
    amount= models.IntegerField(validators=[MinValueValidator(0)])
    description=models.TextField()
    strength = models.PositiveIntegerField()
    speed = models.PositiveIntegerField() 
    potential = models.PositiveIntegerField() 
    intelligence = models.PositiveIntegerField() 
    endurance = models.PositiveIntegerField() 
    height = models.DecimalField(max_digits=5, decimal_places=2)
    weight = models.DecimalField(max_digits=5, decimal_places=2)
Kemudian register model yang Anda buat ke admin. Caranya adalah:
from django.contrib import admin
from .models import Item

# Register your models here.
admin.site.register(Item)
Setiap kali Anda selesai mengedit atau membuat models, Anda perlu melakukan hal ini pada directory root project di terminal Anda:
	python manage.py makemigrations
	python manage.py migrate
untuk memperbarui state pada database di django.

E.	Untuk membuat sebuah fungsi pada views.py, Anda perlu navigasi ke views.py pada directory yang sama. Setelah itu buat sebuah fungsi sebagai contoh:

from django.shortcuts import render
from .models import WaifuStatsCard

# Create your views here.
def home(request):
    waifu = Item(
        name="Keqing",
        amount=10,  # Jumlah, pastikan >= 0
        description="Cakep Banget Sumpah Maukah Keqing jadi Istriku?",
        strength=80,
        speed=90,
        potential=85,
        intelligence=75,
        endurance=70,
        height=160.5,  # Tinggi dalam cm
        weight=48.5    # Berat dalam kg
    )
    return render(request, "home.html", {'data': waifu})

Sederhananya fungsi pada views berguna untuk meng-handle url yang dikunjungi oleh pengguna di browser. Url yang tepat akan memanggil fungsi yang tepat pada views.py. 
F.	Agar dapat memanggil fungsi yang tepat untuk setiap permintaan url, maka kita perlu melakukan konfigurasi pada urls.py pada tingkat app, dalam hal ini file urls.py pada aplikasi yang sedang Anda kerjakan, untuk saya yaitu aplikasi main. 
Contohnya seperti ini:

from django.urls import path

from . import views

urlpatterns = [

    path('', views.home, name='home'),  # menambahkan fungsi home untuk handle path url “{urldasar}/”

  ]
G.	Membuat Template. Template adalah file yang berisi markup HTML dan kode template yang digunakan untuk menghasilkan halaman web dinamis dengan menggabungkan data dari server atau sumber data lainnya dengan tampilan HTML yang telah ditentukan sebelumnya. Pada views.home sebelumnya, yaitu
 def home(request):
    waifu = Item(
        name="Keqing",
        amount=10,  # Jumlah, pastikan >= 0
        description="Cakep Banget Sumpah Maukah Keqing jadi Istriku?",
        strength=80,
        speed=90,
        potential=85,
        intelligence=75,
        endurance=70,
        height=160.5,  # Tinggi dalam cm
        weight=48.5    # Berat dalam kg
    )
    return render(request, "home.html", {'data': waifu})

home.html adalah salah satu contoh template. Cara membuatnya adalah Anda perlu membuat sebuah folder bernama templates di direktori yang sama dengan folder views tersebut, kemudian di dalam folder templates, Anda bisa menambahkan file html bernama home.html.

Bagi saya, kode home.html adalah sebagai berikut:

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Waifu Card</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-gray-100">
    <div class="container mx-auto mt-8">
        <!-- Card Container -->
        <div class="max-w-lg mx-auto bg-white rounded-lg shadow-lg overflow-hidden">
            <!-- Card Header -->
            <div class="bg-gradient-to-r from-purple-400 to-pink-500 p-4">
                <h1 class="text-2xl font-semibold text-white">Waifu Card</h1>
            </div>
            <!-- Card Body -->
            <div class="p-4">
                <!-- Waifu Name -->
                <h2 class="text-xl font-semibold text-gray-800 mb-2">{{ data.name }}</h2>
                <!-- Waifu Description -->
                <p class="text-gray-600">{{ data.description }}</p>
                <!-- Waifu Stats -->
                <div class="mt-4">
                    <h3 class="text-lg font-semibold text-gray-800">Stats:</h3>
                    <ul class="list-disc list-inside text-gray-600">
                        <li>Strength: {{ data.strength }}</li>
                        <li>Speed: {{ data.speed }}</li>
                        <li>Potential: {{ data.potential }}</li>
                        <li>Intelligence: {{ data.intelligence }}</li>
                        <li>Endurance: {{ data.endurance }}</li>
                    </ul>
                </div>
                <!-- Waifu Physical Attributes -->
                <div class="mt-4">
                    <h3 class="text-lg font-semibold text-gray-800">Physical Attributes:</h3>
                    <ul class="list-disc list-inside text-gray-600">
                        <li>Height: {{ data.height }} cm</li>
                        <li>Weight: {{ data.weight }} kg</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</body>
</html>

H.	Langkah terakhir adalah melakukan deployment ke platform hosting, misal Adaptable.io . Akan tetapi, sebelum Anda melakukannya, Anda perlu melakukan navigasi ke settings.py pada directory tingkat project Anda. Lalu pastikan line ini: 
ALLOWED_HOSTS = ["*"]
Hal tersebut berguna agar django mengizinkan domain atau host mana yang diizinkan untuk mengakses aplikasi Anda setelah Anda mendeploynya ke internet. “*” artinya apapun itu boleh. Silahkan deploy ke platform kesukaan Anda.

2.
![Bagan](https://github.com/isaui/WaifuCollection/blob/9fe8797606c2b451c87029757275c1cb5ecf1870/huh.png)

urls.py:
file urls.py adalah tempat untuk mendefinisikan rute untuk aplikasi pada projek django. Terdapat dua urls.py, yaitu urls.py yang berada di level projek dan urls.py yang berada di level aplikasi. urls.py yang berada di level projek berfungsi sebagai root yang digunakan untuk mendefinisikan rute tiap aplikasi atau dengan kata lain menghubungkan rute dasar dengan rute yang didefiniikan di urls.py yang berada di tingkat aplikasi. Sebagai contoh rute aplikasi admin memiliki awalan rute ‘/admin’, rute aplikasi main memiliki awalan rute ‘’, dan rute aplikasi chat memiliki awalan rute ‘/chat’ dan sebagainya.
File urls.py pada level aplikasi digunakan untuk menghubungkan rute spesifik untuk setiap aplikasi dengan fungsi views pada apliaksi tersebut yang sesuai. Rute pada aplikasi ini tentu saja mewarisi rute dasar yang sudah didefinisikan oleh file urls.py yang berada pada tingkat projek.
views.py:
File views.py berisi definisi fungsi-fungsi yang akan menangani permintaan klien. Pada file ini, kita dapat mengakses models dan memodifikasinya. Selain itu, kita juga dapat menentukan template yang harus dirender sesuai request tertentu.
models.py:

File models.py berisi definisi model atau struktur  untuk data pada aplikasi. Model juga merupakan representasi dari tabel di database dalam bentuk objek dan kelas di python. Model ini digunakan oleh views untuk mengambil, menyimpan, atau memanipulasi data dalam database.
Berkas HTML:
Berkas html pada django bisa dikatakan sebagai template yang berisi tampilan yang akan dikirimkan ke klien sebagai respons. Template HTML ini berisi markup dan sintaksis untuk menampilkan data dinamis yang diberikan oleh Views. Views menggunakan template ini untuk merender tampilan HTML yang akan dikirimkan ke klien sebagai respon.
Kaitan:
a.	Permintaan klien pertama kali mencocokkan URL yang dikirimkan ke urls.py.
b.	urls.py mengarahkan permintaan ke tampilan (views) yang sesuai.
c.	Fungsi di views.py menerima permintaan, berinteraksi dengan Model (jika perlu) untuk mengambil atau memanipulasi data, dan merender template HTML.
d.	Template HTML digunakan untuk merender tampilan akhir yang dikirimkan sebagai respons ke klien.

3. Kita perlu menggunakan virtual environment karena virtual environment memungkinkan kita untuk mengisolasi suatu proyek aplikasi. Dengan mengisolasinya, maka kita tidak perlu khawatir bahwa dependensi paket ataupun versi pada proyek tersebut akan saling bertentangan atau mempengaruhi proyek-proyek lainnya. Hal tersebut dapat mengatasi terjadinya resiko konflik antar proyek. Salah satu contohnya adalah kita dapat menggunakan versi django dan python yang berbeda pada projek yang berbeda.
Kita tetap dapat membuat projek django tanpa menggunakan virtual environment. Akan tetapi, resiko konflik dependensi akan mengintai projek kita. Hal tersebut karena apabila django pada projek kita berjalan pada versi x, namun django pada environment user berjalan pada versi y, maka hal tersebut dapat menyebabkan konflik dependensi. Hal yang sama berlaku untuk paket yang lain.
4. MVC, MVT, dan MVVM adalah pola desain (design pattern) yang digunakan dalam pengembangan perangkat lunak untuk mengorganisasi kode menjadi struktur yang lebih terstruktur dan mudah dikelola.
MVC atau Model View Controller adalah pola desain dalam membuat aplikasi dengan memisahkan kode menjadi tiga bagian utama yaitu Model, View, dan Controller. Model adalah bagian yang bertugas sebagai representasi data  dan untuk melakukan CRUD pada database. View adalah bagian yang bertugas menampilkan data aplikasi dalam bentuk Graphical User Interface (GUI). Sementara Controller adalah penghubung antara Model dan View. Controller berfungsi menerima dan memproses input user dan kemudian menghubungkan ke model untuk mengupdate database ataupun menghubungkan ke View untuk menampilkan view atau tampilan yang sesuai.
MVT atau Model View Template adalah pola desain dalam membuat aplikasi yang memisahkan kode menjadi tiga bagian utama, yaitu Model, View, dan Template. MVT merupakan pengembangan lebih lanjut dari MVC. Pada MVT, Model dan View sudah saling terhubung, berbeda dengan MVC yang mana Model dan View terisolasi satu sama lain. Kemudian, terdapat Template yang mana berfungsi untuk menampilkan tampilan atau Graphical User Interface (GUI) yang dinamis berdasarkan data yang dikirim dari View. Untuk Model, tidak ada perbedaan signifikan dengan Model di MVT. View di MVT bertugas untuk mengambil data dari Model dan menyiapkan data tersebut untuk ditampilkan dalam Template.
MVVM atau Model View View-Model adalah pola desain dalam membuat aplikasi yang memisahkan kode menjadi tiga bagian utama, yaitu Model, View, dan ViewModel. Pola desain ini memisahkan business logic dengan GUI. Model / entity adalah representasi dari data yang digunakan pada business logic. View adalah UI atau tampilan dari aplikasi itu sendiri dan berinteraksi langsung dengan user. View-Model adalah layer yang berfungsi untuk mengambil data dari Model dan mengirimkannya ke View untuk ditampilkan ke user. View-Model berperan sebagai perantara untuk data-binding yang mana View akan berubah otomatis sesuai dengan perubahan data pada model. ViewModel menghubungkan Model dengan View dan memastikan bahwa perubahan data pada Model tercermin secara real-time dalam tampilan aplikasi.
Perbedaan antara ketiganya adalah MVC memisahkan aplikasi menjadi Model, View, dan Controller dengan Controller sebagai perantara antara Model dan View. MVT, yang merupakan perkembangan dari MVC, menghubungkan Model dan View secara erat dan memanfaatkan Template untuk merender tampilan. Sementara itu, MVVM memisahkan Model, View, dan ViewModel, dengan ViewModel yang memfasilitasi pengikatan data, memungkinkan tampilan untuk berubah otomatis sesuai dengan perubahan data pada Model, sehingga membuat aplikasi lebih reaktif dan mudah diuji.
