BILGINET API
------------
------------

Dökümantasyon
-------------

- Kod örnekleri,gönderilecek veri tipleri,veri alanları vs. 
- Önemli olan alanlar renkli olarak yazılmıştır.

Özellikler
----------

- İstek Adresi	: http://www.example.com/extended/api/v1/json|xml/İstek
- İstek Formatı	: JSON / XML
- Cevap Formatı	: JSON / XML
- API VERSIYON	: 0.60

Doğrulama
---------

- Basit HTTP Doğrulama 
- Doğrulama için : Kullanıcı Adı ve Şifre Gereklidir
	- `curl \ --header "Content-type: application/json" \ --request POST \ --data '{"user": "John", "password": "doe"}' \ http://www.example.com/extended/api/v1/json/ApiLogin`
- Kullanıcı Bilgilerinizi almak için lütfen site yöneticisi ile görüşünüz

### Kullanıcı Tipleri
- `api` Sadece api üzerinden login olabilir ve admin in verdiği yetkilerce ekleme, düzenleme, listeleme ve silme işlemlerini yapabilir.

Özellikler
----------

- Canlı
- Test Ortamı `Şuan da yapım aşamasında `

Cevap Öğeleri
-------------

BILGINET API sistemi size `JSON` veya `XML` formatın da bilgi geri dönecektir. Bu değer `sizin API isteğini hangi formatta` yaptığınız ile değişiklik göstermektedir.
Geri Dönen Cevaplar içerisinde `status` 0 ise bir sorun ile karşılaşılmış; `status` 1 ise işleminiz başarı ile gerçekleştirilmiştir.
İşlem başarı ile gerçekleştiği takdir `error` ve `error_code` alanları size `NULL` olarak dönecektir.

### Cevap Örnekleri

- Başarılı bir istek için cevap isteği aşağıda ki gibidir

```
	{
		"status"	 : 1,
		"result"	 : {"DeleteProduct":1},
		"error"		 : NULL,
		"error_code" : NULL
	}

```

- Başarısız veya Hata ile sonuçlanan bir istek için cevap örneği aşağıdaki gibidir.

```
	{
		"status"	 : 0,
		"result"	 : {"DeleteProduct":0},
		"error"		 : "Ürün Silme İşleminde Hata",
		"error_code" : 0041
	}

```

ÜRÜN İŞLEMLERİ
--------------
--------------

- `Login oluşturduğunuz token mutlaka gönderilmelidir.`
- * alanlar zorunlu alanlardır
- [opt] Opsiyonel alanlardır
- Açık veya Kapalı, Var veya Yok durumunda işlem yapan alanlar her zaman aşağıdaki değerleri alırlar
	- 0 = Var / Açık
	- 1 = Yok / Kapalı


### EKLEME İstek /AddProduct

	- `token` *mixed 32* * * *
	- `ProductName` *varchar 200* * * *
	- `ProductSalePrice` *text* * * *
	- `ProductCategories` *array->int* * * *
	- `ProductOrder` *mediumint 6* *[opt]*
	- `ProductType` *int 1* *[opt]*
		- Ürün Tipinin Ne olduğunu belirlemenize yarar. Örneğin : 0=Ürün,1=Asorti,2=Paket
	- `ProductShrtText` * text * *[opt]*
	- `ProductStatus` *int 1* *[opt]*
		- Aksi Belirtilmedikçe Varsayılan olarak 0=> Kapalı Değerini alır
	- `ProductText` * longtext * *[opt]* 
	- `ProductCode` * varchar 128 * *[opt]*
	- `ProductStrichCode` *varchar 64* *[opt]*
	- `ProductCostPrice` *float 7,2* *[opt]*
	- `ProductProfitRate` *int 4* *[opt]*
	- `ProductTaxRate` *int 2* *[opt]*
	- `ProductPrice` *float 7,2* *[opt]*
	- `ProductMarketPrice` *float 7,2* *[opt]*
	- `ProductOldPrice` *float 7,2* *[opt]*
	- `ProductTransferPrice` *float 7,2* *[opt]*
	- `ProductWholeAllPrice` *float 7,2* *[opt]*
	- `ProductDealerPrice` *float 7,2* *[opt]*
	- `ProductCurrency` *string 3* *[opt]*
		- UluslarArası ParaBirimi Kodları Geçerlidir.Örneğin: `TRY`,`USD`,`EUR`
	- `ProductStockAmount` *int 6* *[opt]*
		- Eğer değer gönderilmez ise StokDışı olucaktır.
	- `ProductShowCase` *int 1* *[opt]*
		- Vitrinde Gösterilsin mi?
	- `ProductOpportunity` *int 1* *[opt]*
		-Fırsat Ürünü mü ? 
	- `ProductFreeShip` *int 1* *[opt]*
		- Ücretsiz Kargo Mu?
	- `ProductShipTime` *int 2* *[opt]*
	- `ProductFreeInsTime` *int 1* *[opt]*
		- Ücretsiz Montaj Var mı ?
	- `ProductGuarantee` *int 1* *[opt]*
		- 24 Ay Garantiye Dahil mi ?
	- `ProductEditorChoice` *int 1* *[opt]*
		- Editor Seçimi mi ?
	- `ProductFastShip` *int 1* *[opt]*
		- Bu üründe hızlı kargo var mı ? 
	- `ProductSameDayDelivery` *int 1* *[opt]*
		- Aynı Gün Teslimat Var Mı?
	- `ProductDiscounted` *int 1* *[opt]*
		-İndirimli Ürün mü ?
	- `ProductDiscountRate` *int 2* *[opt]*
		-indirim Oranı
	- `ProductBundle` *int 1* *[opt]*
		- Hediyeli Ürün mü ?
	- `ProductGifts` *string* *[opt]*
		-Hediyeler
	- `ProductBrandID` *int 4* *[opt]*
	- `ProductSupplierID` *int 4* *[opt]*
	- `ProductUnit` *int 2* *[opt]*
		- Ürün Birimi 
			- 1 => Adet
			- 2 => Kilogram
			- 3 => Metre
			- 4 => MetreKare
			- 5 => Litre
			- 6 => Koli
	- `ProductBuyMin` *int 5* *[opt]*
		-Minimum Satın Alınacak Miktar
	- `ProductBuyIncrease` *int 5* *[opt]*
		- Sepet artış Miktarı
	- `ProductSeoTitle` *varchar 255* *[opt]*
	- `ProductSeoText` *varchar 255* *[opt]*
	- `ProductSeoKeyword` *varchar 255* *[opt]*


### Ürün Ekleme Cevap

	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"AddProduct":ID},
				"error"		 : NULL,
				"error_code" : NULL
			}

		```
### Ürün Listeleme İstek /ListProduct

	- `token` *mixed 32* ***
	- `ID` *int* *[opt]*
	- `ProductName` *varchar* *[opt]*
	- `ProductOrderBy` *varchar* *[opt]*
	- `ProductStatus` *int* *[opt]*
		- 0 / 1

### Ürün Listeleme Cevap
	
	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"ListProduct": 
									{"ID" : `Eklemede Gönderilen Tüm Değerler`}
								},
				"error"		 : NULL,
				"error_code" : NULL
			}

		```
### Ürün Düzenleme İstek /EditProduct
	
	- `token` *mixed 32* ***
	- `ID` *int* ***
	- `ProductName` *varchar 200* * * *
	- `ProductSalePrice` *text* * * *
	- `ProductCategories` *array->int* * * *
	- `ProductOrder` *mediumint 6* *[opt]*
	- `ProductType` *int 1* *[opt]*
		- Ürün Tipinin Ne olduğunu belirlemenize yarar. Örneğin : 0=Ürün,1=Asorti,2=Paket
	- `ProductShrtText` * text * *[opt]*
	- `ProductStatus` *int 1* *[opt]*
		- Aksi Belirtilmedikçe Varsayılan olarak 0=> Kapalı Değerini alır
	- `ProductText` * longtext * *[opt]* 
	- `ProductCode` * varchar 128 * *[opt]*
	- `ProductStrichCode` *varchar 64* *[opt]*
	- `ProductCostPrice` *float 7,2* *[opt]*
	- `ProductProfitRate` *int 4* *[opt]*
	- `ProductTaxRate` *int 2* *[opt]*
	- `ProductPrice` *float 7,2* *[opt]*
	- `ProductMarketPrice` *float 7,2* *[opt]*
	- `ProductOldPrice` *float 7,2* *[opt]*
	- `ProductTransferPrice` *float 7,2* *[opt]*
	- `ProductWholeAllPrice` *float 7,2* *[opt]*
	- `ProductDealerPrice` *float 7,2* *[opt]*
	- `ProductCurrency` *string 3* *[opt]*
		- UluslarArası ParaBirimi Kodları Geçerlidir.Örneğin: `TRY`,`USD`,`EUR`
	- `ProductStockAmount` *int 6* *[opt]*
		- Eğer değer gönderilmez ise StokDışı olucaktır.
	- `ProductShowCase` *int 1* *[opt]*
		- Vitrinde Gösterilsin mi?
	- `ProductOpportunity` *int 1* *[opt]*
		-Fırsat Ürünü mü ? 
	- `ProductFreeShip` *int 1* *[opt]*
		- Ücretsiz Kargo Mu?
	- `ProductShipTime` *int 2* *[opt]*
	- `ProductFreeInsTime` *int 1* *[opt]*
		- Ücretsiz Montaj Var mı ?
	- `ProductGuarantee` *int 1* *[opt]*
		- 24 Ay Garantiye Dahil mi ?
	- `ProductEditorChoice` *int 1* *[opt]*
		- Editor Seçimi mi ?
	- `ProductFastShip` *int 1* *[opt]*
		- Bu üründe hızlı kargo var mı ? 
	- `ProductSameDayDelivery` *int 1* *[opt]*
		- Aynı Gün Teslimat Var Mı?
	- `ProductDiscounted` *int 1* *[opt]*
		-İndirimli Ürün mü ?
	- `ProductDiscountRate` *int 2* *[opt]*
		-indirim Oranı
	- `ProductBundle` *int 1* *[opt]*
		- Hediyeli Ürün mü ?
	- `ProductGifts` *string* *[opt]*
		-Hediyeler
	- `ProductBrandID` *int 4* *[opt]*
	- `ProductSupplierID` *int 4* *[opt]*
	- `ProductUnit` *int 2* *[opt]*
		- Ürün Birimi 
			- 1 => Adet
			- 2 => Kilogram
			- 3 => Metre
			- 4 => MetreKare
			- 5 => Litre
			- 6 => Koli
	- `ProductBuyMin` *int 5* *[opt]*
		-Minimum Satın Alınacak Miktar
	- `ProductBuyIncrease` *int 5* *[opt]*
		- Sepet artış Miktarı
	- `ProductSeoTitle` *varchar 255* *[opt]*
	- `ProductSeoText` *varchar 255* *[opt]*
	- `ProductSeoKeyword` *varchar 255* *[opt]*


### Ürün Düzenleme Cevap
	
	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"EditProduct": 
									{"ID" : `0 veya 1 değeri`}
								},
				"error"		 : NULL,
				"error_code" : NULL
			}

		```
### Ürün Silme İstek /DeleteProduct

	- `token` *mixed 32* ***
	- `ID` *String veya Array*
		- Array Formtı : array(23,5,14,16)
	
### Ürün Silme Cevap
	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"DeleteProduct": ID => `0 veya 1 değeri`},
				"error"		 : NULL,
				"error_code" : NULL
			}
		```

MARKA İŞLEMLERİ
--------------
--------------

- `Login oluşturduğunuz token mutlaka gönderilmelidir.`
- * alanlar zorunlu alanlardır
- [opt] Opsiyonel alanlardır
- Açık veya Kapalı, Var veya Yok durumunda işlem yapan alanlar her zaman aşağıdaki değerleri alırlar
	- 0 = Var / Açık
	- 1 = Yok / Kapalı


###MARKA EKLEME /AddBrand

	- `token` *mixed 32* ***
	- `BrandName` *varchar 200* ***
	- `BrandStatus` *int 1* 
	- `BrandOrder` *int 1*
	- `BrandText` *text*
	- `BrandSeoTitle` *varchar 255*
	- `BrandSeoText` *varchar 255*
	- `BrandSeoKeyword` *text*

###MARKA EKLEME Cevap
	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"AddBrand":ID},
				"error"		 : NULL,
				"error_code" : NULL
			}

		```
###MARKA DÜZENLE /EditBrand

	- `token` *mixed 32* ***
	- `ID` *int 2* ***
	- `BrandName` *varchar 200* ***
	- `BrandStatus` *int 1* 
	- `BrandOrder` *int 1*
	- `BrandText` *text*
	- `BrandSeoTitle` *varchar 255*
	- `BrandSeoText` *varchar 255*
	- `BrandSeoKeyword` *text*

###MARKA DÜZENLE Cevap
	
	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"EditBrand": ID => `0 veya 1 değeri`},
				"error"		 : NULL,
				"error_code" : NULL
			}

###MARKA LİSTELE /ListBrand
	
	- `token` *mixed 32* ***
	- `BrandName` *varchar 200* ***
	- `BrandStatus` *int 1* 
	- `BrandOrderBy` *int 1*

###MARKA LİSTELE CEVAP

	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"ListBrand": 
									{"ID" : `Eklemede Gönderilen Tüm Değerler`}
								},
				"error"		 : NULL,
				"error_code" : NULL
			}

		```

###MARKA SİLME /DeleteBrand
	
	- `token` *mixed 32* ***
	- `ID` *int 1* ***

###MARKA SİLME Cevap
	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"DeleteBrand": `0 veya 1 değeri`},
				"error"		 : NULL,
				"error_code" : NULL
			}
		```

KATEGORİ İŞLEMLERİ
--------------
--------------

- `Login oluşturduğunuz token mutlaka gönderilmelidir.`
- * alanlar zorunlu alanlardır
- [opt] Opsiyonel alanlardır
- Açık veya Kapalı, Var veya Yok durumunda işlem yapan alanlar her zaman aşağıdaki değerleri alırlar
	- 0 = Var / Açık
	- 1 = Yok / Kapalı


###KATEGORİ EKLEME /AddCategory

	- `token` *mixed 32* ***
	- `CategoryName` *varchar 200* ***
	- `CategoryStatus` *int 1* 
	- `CategoryOrder` *int 1*
	- `CategoryText` *text*
	- `CategoryParent` *int 4* 
	- `CategorySeoTitle` *varchar 255*
	- `CategorySeoText` *varchar 255*
	- `CategorySeoKeyword` *text*

###KATEGORİ EKLEME Cevap
	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"AddBrand":ID},
				"error"		 : NULL,
				"error_code" : NULL
			}

		```
###KATEGORİ DÜZENLE /EditCategory

	- `token` *mixed 32* ***
	- `ID` *int 2* ***
	- `CategoryName` *varchar 200* ***
	- `CategoryStatus` *int 1* 
	- `CategoryOrder` *int 1*
	- `CategoryText` *text*
	- `CategoryParent` *int 4* 
	- `CategorySeoTitle` *varchar 255*
	- `CategorySeoText` *varchar 255*
	- `CategorySeoKeyword` *text*

###KATEGORİ DÜZENLE Cevap
	
	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"EditCategory": ID => `0 veya 1 değeri`},
				"error"		 : NULL,
				"error_code" : NULL
			}

###KATEGORİ LİSTELE /ListCategory
	
	- `token` *mixed 32* ***
	- `CategoryName` *varchar 200* ***
	- `CategoryStatus` *int 1* 
	- `CategoryOrderBy` *int 1*

###KATEGORİ LİSTELE CEVAP

	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"ListCategory": 
									{"ID" : `Eklemede Gönderilen Tüm Değerler`}
								},
				"error"		 : NULL,
				"error_code" : NULL
			}

		```

###KATEGORİ SİLME /DeleteCategory
	
	- `token` *mixed 32* ***
	- `ID` *int 1* ***

###KATEGORİ SİLME Cevap
	- JSON / XML
		- ```
			{
				"status"	 : 1,
				"result"	 : {"DeleteCategory": `0 veya 1 değeri`},
				"error"		 : NULL,
				"error_code" : NULL
			}
		```


