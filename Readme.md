# Ringkasan Pesanan
Ringkasan Pesanan adalah sebuah aplikasi sederhana yang digunakan untuk memesan beberapa makanan dan menampilkan total harga yang harus dibayarkan. Pada aplikasi ini terdapat konsep MVC (Model View Controller).

## Scope & Functionalities
- User dapat menekan tombol + untuk memilih menu yang telah tersedia pada aplikasi
- User dapat menghapus menu yang sebelumnya telah ditambahkan

## How Does It Work ?
Pada saat user ingin membuka list menu dengan menekan button +, sebuah method telah dibuat untuk menampilkan list menu tersebut. Berikut source codenya
```csharp
private void onButtonAddItemClicked(object sender, RoutedEventArgs e)
        {
            Penawaran penawaranWindow = new Penawaran();
            penawaranWindow.SetOnItemSelectedListener(this);
            penawaranWindow.Show();
        }
```
Ada juga method yang terdapat pada `KeranjangBelanja.cs` digunakan untuk melakukan penambahan item ke keranjang belanja dan menghitung subTotal. Berikut source codenya
```csharp
public void addItem(Item item)
        {
            this.itemBelanja.Add(item);
            this.callback.addItemSucceed();
            calculateSubTotal();
        }
```
Kemudian di `KeranjangBelanja.cs` terdapat juga method yang digunakan menghapus item yang sebelumnya telah di tambahkan dalam keranjang belanja. Berikut source codenya
```csharp
public void removeItem(Item item)
        {
            this.itemBelanja.Remove(item);
            this.callback.removeItemSucceed();
            calculateSubTotal();
        }
```
Untuk perhitungan total keseluruhan harga dari item-item yang telah ditambahkan maka dilakukan perhitungan `subTotal - delivery fee + promo`
```csharp
public void updateTotal(double subtotal)
        {
            double total = subtotal + deliveryFee - promo;
            this.balance = this.balance - total;
            this.paymentCallback.onPriceUpdated(subtotal, total, balance);
        }
```
Dan terakhir untuk mengganti list menu yang telah tersedia yaitu dengan cara merubah list menunya yang terdapat pada source code berikut ini
```csharp
private void generateContentPenawaran()
        {
            Item drink1 = new Item("Ice tea", 8000);
            Item drink2 = new Item("Ice lemon tea", 5000);
            Item drink3 = new Item("Ice lemon", 7000);
            Item food4 = new Item("Bakso", 17000);
            Item food5 = new Item("Gado-gado", 14000);
            Item food6 = new Item("Sate", 15000);

            controller.addItem(drink1);
            controller.addItem(drink2);
            controller.addItem(drink3);
            controller.addItem(food4);
            controller.addItem(food5);
            controller.addItem(food6);

            listPenawaran.Items.Refresh();
        }
```