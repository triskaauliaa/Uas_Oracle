# Project UAS Pemrosesan Data Tersebar (PDT)

Membuat aplikasi Pembelian dan Penjualan dengan database Oracle dengan System Administrator menggunakan PHP dan Antar Muka di Mobile Apps atau Android. Komunikasi data antar aplikasi menggunakan Restfull API yang dibuat di Oracle.



# Requirements / Persyaratan

-   [Virtual Box](https://www.virtualbox.org/wiki/Downloads)  (Virtual Server)
-   [Oracle Developer Day 11g](https://www.oracle.com/technetwork/database/enterprise-edition/databaseappdev-vm-161299.html)  (Database)
-   [Android Studio](https://developer.android.com/studio)  (Android IDE)
-   [Codeigniter](https://www.codeigniter.com/)  (Framework PHP)

## TUTORIAL

### Database
Aplikasi ini memiliki 5 table, yaitu :

1.  [Customer](#table-customer)
2.  [Barang](#table-barang)
3.  [Supplier](#table-supplier)
4.  [Pembelian](#table-pembelian)
5.  [Penjualan](#table-penjualan)



## Table Barang

![Table Barang!](./Barang/barang.png "Table Barang")

## Table Customer

![Table Customer!](./Customer/customer.png "Table Customer")

## Table Supplier

![Table Supplier!](./Supplier/supplier.png "Table Supplier")

## Table Pembelian

![Table Pembelian!](./Pembelian/pembelian.png "Table Pembelian")

## Table Penjualan

![Table Penjualan!](./Penjualan/penjualan.png "Table Penjualan")

## *RESTful Service*

![Table Restful!](./restful.png "Table RESTful")

PUT dan DELETE menggunakan {id} untuk mengidentifikasi data yang akan dieksekusi.  
Metode HTTP yang digunakan dalam aplikasi ini adalah:

| Method | Description |
| ------ | ------ |
| **GET** | Menyediakan hanya akses baca pada _resource_ |
| **POST** | Digunakan untuk menciptakan _resource_ baru |
| **PUT** | Digunakan untuk memperbarui _resource_ yang ada atau membuat _resource_ baru |
| **DELETE** | Digunakan untuk menghapus _resource_ |

*Resource Handler* & *Query* dapat dilihat pada gambar dibawah ini.

#### *RESTful Service* pada Barang

- **GET Barang**  
![GET](./Barang/get_barang.png)

- **POST Barang**  
![POST](./Barang/post_barang.png)

- **PUT Barang**  
![PUT](./Barang/put_barang.png)

- **DELETE Barang**  
![DELETE](./Barang/delete_barang.png)

#### *RESTful Service* pada Customer

- **GET Customer**  
![GET](./Customer/get_customer.png)

- **POST Customer**  
![POST](./Customer/post_customer.png)

- **PUT Customer**  
![PUT](./Customer/put_customer.png)

- **DELETE Customer**  
![DELETE](./Customer/delete_customer.png)

#### *RESTful Service* pada Supplier

- **GET Supplier**  
![GET](./Supplier/get_supplier.png)

- **POST Supplier**  
![POST](./Supplier/post_supplier.png)

- **PUT Supplier**  
![PUT](./Supplier/put_supplier.png)

- **DELETE Supplier**  
![DELETE](./Supplier/delete_supplier.png)

#### *RESTful Service* pada Pembelian

- **GET Pembelian**  
![GET](./Pembelian/get_pembelian.png)

- **POST Pembelian**  
![POST](./Pembelian/post_pembelian.png)

#### *RESTful Service* pada Penjualan

- **GET Penjualan**  
![GET](./Penjualan/get_penjualan.png)

- **POST Penjualan**  
![POST](./Penjualan/post_penjualan.png)

### CodeIgniter

[Script](./oracle-uas/application/libraries/Api.php) dibawah ini merupakan script php yang digunakan untuk mengakses *RESTful Services* dari Oracle menggunakan library [Goutte](https://github.com/FriendsOfPHP/Goutte).

```php
use GuzzleHttp\Client;

defined('BASEPATH') or exit('No direct script access allowed');

class Api
{
    private $client;

    public function __construct()
    {
        // base url yang digunakan untuk mengakses RESTful API
        $this->client = new Client(['base_uri' => 'http://192.168.43.75:8888/apex/obe/']);
    }

    public function request($method, $uri, $data = [])
    {
        // data di convert menjadi data JSON
        $options['json'] = $data;

        // jika metode HTTP nya adalah DELETE maka response yang diberikan adalah status code nya
        if ($method == 'delete') {
            $request = $this->client->request($method, $uri);
            return $request->getStatusCode();
        }

        $request = $this->client->request($method, $uri, $options);

        // response yang diberikan berupa content nya
        return $request->getBody()->getContents();
    }
}
```

#### Tampilan Web

- Barang
![List Barang](./Barang/barang2.png)

- Customer
![List Customer](./Customer/customer2.png)

- Supplier
![List Supplier](./Supplier/supplier2.png)

- Pembelian
![List Pembelian](./Pembelian/pembelian2.png)

- Penjualan
![List Penjualan](./Penjualan/penjualan2.png)

#### Tampilan Mobile Apps

![Gambar Android](./Customer/android.png)









```
