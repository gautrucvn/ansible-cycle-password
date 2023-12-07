# CHANGE ROOT PASSWORD HASH AND STORED IT

## Khai báo các biến trong Ansible Playbook
passwdDir: Khai báo vị trí lưu backup encrypt password sau mỗi lần chạy script
vaultPass: Khai báo file lưu keypair sử dụng để mã hóa mật khẩu bằng ansible vault

## Mô tả các Tasks
- Generate root password: Tạo mật khẩu ngẫu nhiên và lưu vào file secret.yaml
** chars=ascii_letters,digits,punctuation ** đề cập tới cách tạo mật khẩu bao gồm ký tự ascii, chữ số và ký tự đặc biệt
- Check if secret.yaml file exists: Kiểm tra rằng file secret tồn tại. lưu lại giá trị này vào biến stat_secrets để thực hiện cho các bước sau
- Update root password hash: Thực hiện việc cập nhật password cho user root
- Encrypt password file using ansible-vault: Mã hóa password bằng ansible Vault và lưu lại giá trị mã hóa vào file secret.yaml
- Get timestamp from the system: lấy giá trị thời gian trên hệ thống
- Save password file to backup using timestamp: Thực hiện backup file lưu mật khẩu root hiện tại

## Xem lại mật khẩu đã lưu trữ trước đó

```
ansible-vault view ~/.secret-yaml-files/secret.yaml-2023-12-07-16.25.29 --vault-password-file ~/.vault_key
```
