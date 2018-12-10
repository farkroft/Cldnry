# Create Cloudinary Account
- Pertama-tama untuk menggunakan image hosting cloudinary, buatlah akun di cloudinary
- Lalu masuk ke menu tab dashboard
- Kemudian pada form Account Details, download file yml accountmu lewat tombol tulisan YML di pojok kanan form tersebut
- Pastikan file cloudinary.yml sudah terdownload

# Initial 
Pindah ke project kamu :
Lalu tambahkan gem di file Gemfile mu
```
gem 'carrierwave'
gem 'cloudinary', '~> 1.9.0'
```
kemudian run bundle install
Lalu buka gemfile.lock, search cloudinary di file tersebut
dan pastikan versinya 1.9.1
Lalu masukkan file cloudinary.yml tadi ke dalam projectmu
Yaitu ke directory config

# Buat File untuk uploader
jalankan command berikut :
```
rails g uploader avatar
```
sesuaikan dengan nama column tempat kamu menyimpan image

# edit file di uploader/avatar.rb
Edit file avatar.rb yang baru saja kamu buat
Command semua code, kecuali class
Lalu tambahkan code di line 5 :
```
include Cloudinary::CarrierWave
```
# edit model
Edit model yang berhubungan dengan image mu
Tambahkan code ini :
```
mount_uploader :avatar, AvatarUploader
```
Sesuaikan dengan file upload milikmu yang tadi kamu buat

# Edit controller
Edit controllermu dan tambahkan method untuk create
```
def create
 @user = User.new(user_params)
   if @user.save
      render json: { result: true, msg: ' The image is sucessfully         uploaded!!'}, status: :created
   else
      render json: {result: false, user: @user.errors }, status:          :unprocessable_entity
   end
 end
 
private
def user_params
 params.permit(:name, :avatar)
end
 ```
 # Coba test menggunakan postman
 Test post menggunakan postman

 
