# Promos 2
aplikasi ini merupakan lanjutan promos pertama yang disempurnakan atau ditambahkan lebih mudah digunakan 

## Scope & Functionalities
- User dapat melihat daftar makanan yang ditawarkan 
- User dapat memasukkan atau menghapus makanan pilihan ke dalam keranjang - User dapat melihat subtotal makanan yang terdapat pada keranjang 
- User dapat melihat daftar voucher yang ditawarkan 
- User dapat menggunakan salah satu voucher 
- User dapat melihat harga total termasuk potongannya 

## How Does it Works ?
Diawali method `MainWindow` pada class `MainWindow.xaml.cs` kita mendeklarasikan dengan 

``` csharp
  public MainWindow()
        {
            InitializeComponent();

            payment = new Payment(this);
            payment.setBalance(500000);
            payment.setPromo(0);

            KeranjangBelanja keranjangBelanja = new KeranjangBelanja(payment, this);

            controller = new MainWindowController(keranjangBelanja);

            listBoxPesanan.ItemsSource = controller.getSelectedItems();
            listBoxPakaiVoucher.ItemsSource = controller.getSelectedVouchers();

            initializeView();

        }
```

logika voucher di deklarasikan dengan class `PilihVoucher.xaml.cs` dengan source code
``` csharp
 public PilihVoucher()
        {
            InitializeComponent();

            voucherController = new Controller.VoucherController();
            DaftarVoucher.ItemsSource = voucherController.getItems();

            generateListVoucher();
        }

        private void generateListVoucher()
        {
            Model.Voucher awalTahun = new Model.Voucher(title: "Promo Awal Tahun Diskon 25%", discInPercent: 25);
            Model.Voucher tebusMurah = new Model.Voucher(title: "Promo Tebus Murah Diskon 30% atau max. 30.000", discInPercent: 30);
            Model.Voucher promoNatal = new Model.Voucher(title: "Promo Natal Potongan 10000", disc: 10000);

            voucherController.addItem(awalTahun);
            voucherController.addItem(tebusMurah);
            voucherController.addItem(promoNatal);

            DaftarVoucher.Items.Refresh();
        }
```

dan untuk logika total pembayaranya terdapat di class `Payment.cs`
``` csharp
 public void updateTotal(double subtotal, double potongan)
        {
            double total = subtotal + potongan;
            this.paymentCallback.onPriceUpdated(subtotal,  total, potongan);
        }
```

## Bagaimana anda mereprensentasikan kasus ini dalam sebuah aplikasi berbasis desktop?
1. Mencari kebutuhan yang diinginkan oleh user
2. Mengolah kebutuhan user
3. Membuat prototype
4. Mencari problem
5. Mengkaji ulang
6. Lalu mengeksekusi program

Kesimpulanya, kita mencari tahu apa yg diinginkan user kemudian carilah solve problem nya.