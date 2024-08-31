// quanlysinhvien
// Quản lý sinh viên gọn nhất 
#include<iostream>
#include<string>
#include<iomanip>
#include<algorithm>
/* Chuong trinh quan ly sinh vien: ho ten, tuoi, gioi tinh, diem
	1 - In danh sach sinh vien
	2 - Them 
	3 - Sua
	4 - Xoa
	5 - Tim Kiem
	6 - Sap xep
	7 - Thong ke
	8 - Sao luu
	9 - Thoat
*/
using namespace std;

class sinh_vien{
	protected:
		string ho_ten, gioi_tinh;
		int tuoi;
		float diem;
	public:
		sinh_vien(){
			this->ho_ten = this->gioi_tinh = " ";
			this->tuoi = 0;
			this->diem = 0;
		}
		~sinh_vien(){
			this->ho_ten = this->gioi_tinh = " ";
			this->tuoi = 0;
			this->diem = 0;
		
		}
		void input(){
			cin.ignore();
			cout << "Nhap ten sinh vien: "; getline(cin, this->ho_ten);
			fflush(stdin);
			cout << "Nhap gioi tinh sinh vien: "; getline(cin, this->gioi_tinh);
			fflush(stdin);
			cout << "Nhap tuoi sinh vien: "; cin >> this->tuoi;
			cout << "Nhap diem sinh vien: "; cin >> this->diem;
		}
		void output(){
			
			cout << "| " << left << setw(18) << this->ho_ten;
			cout << "| " << left << setw(13) << this->gioi_tinh;
			cout << "| " << left << setw(5) << this->tuoi;
			cout << " | " << left << setw(5) << this->diem  << " |"<< endl;
			cout << left << setw(20) << "+---------+-------------------+--------------+-------+-------+" << endl;
		}
		void maintext(){
			cout << left << setw(20) << "+---------+-------------------+--------------+-------+-------+" << endl;
			cout << left << setw(10) << "| STT ";
			cout << left << setw(20) << "| Ho ten ";
			cout << left << setw(15) << "| Gioi tinh";
			cout << left << setw(5) << "| Tuoi ";
			cout << left << setw(5) << " | Diem  |" << endl;
			cout << left << setw(20) << "+---------+-------------------+--------------+-------+-------+" << endl;
		}
		string toLowerCase(string str){
			transform(str.begin(), str.end(), str.begin(), ::tolower);
			return str;
		}
		
		bool SearchByName(string name){
			return toLowerCase(this->ho_ten).find(toLowerCase(name)) != string::npos;
		}
		
		
		
};

int main(){
	int so_luong_sinh_vien;
	int lua_chon;
	cout << "Xin moi nhap so luong sinh vien: ";cin >> so_luong_sinh_vien;
	sinh_vien* sv = new sinh_vien[so_luong_sinh_vien];
	
	
	
	// Nhap du lieu
	for(int i = 0; i < so_luong_sinh_vien; i++) sv[i].input();
	
	do{
		cout << "======  QUAN LY SINH VIEN ======== \n";
		cout << "1 - In danh sach SV " << endl;
		cout << "2 - Them SV" << endl;
		cout << "3 - Sua SV" << endl;
		cout << "4 - Xoa SV" << endl;
		cout << "5 - Tim kiem SV " << endl;
		cout << "6 - Sap xep " << endl;
		cout << "7 - Thong ke " << endl;
		cout << "8 - Sao luu " << endl;
		cout << "9 - Loc " << endl;
		cout << "10 - Thoat " << endl;
		cout << "----------------------------------" <<endl;
		cout << "Xin moi lua chon: "; cin >> lua_chon;
		
		switch(lua_chon){
			case 1:{
				// Tieu de
				sv[so_luong_sinh_vien].maintext();
	
				// Xuat du lieu
	
				for(int i = 0; i < so_luong_sinh_vien; i++){
					cout << "| " << left << setw(8) << i + 1;
					sv[i].output(); 
				}
				break;
			}
			case 2:{
				// Them SV
				so_luong_sinh_vien++;
				sinh_vien* temp = new sinh_vien[so_luong_sinh_vien];
				for(int i = 0; i < so_luong_sinh_vien - 1; i++){
					temp[i] = sv[i];
				}
				delete[] sv;
				sv = temp;
				sv[so_luong_sinh_vien - 1].input();
				break;
			}
			case 3:{
				// Sua SV
				int index;
				cout << "Nhap STT sinh vien muon sua: "; cin >> index;
				if(index > 0 && index <= so_luong_sinh_vien){
					sv[index - 1].input();
				}else{
					cout << "Sinh vien khong ton tai !" << endl;
				}
				break;
			}
				
			case 4:{
				// Xoa SV
				int index;
				cout << "Nhap STT sinh vien muon xoa: "; cin >> index;
				if(index > 0 && index <= so_luong_sinh_vien){
					for(int i = index - 1; i < so_luong_sinh_vien - 1; i++){
						sv[i] = sv[i + 1];
					}
					so_luong_sinh_vien--;
				}		
				else{
					cout << "Sinh vien khong ton tai !" << endl;
					
				}
				break;
			}
			case 5:{
				string searchName;
				cout << "Nhap sinh vien muon tim: "; 
				cin.ignore(); 
				getline(cin, searchName);
				
				bool found = false;
				for(int i = 0; i < so_luong_sinh_vien; i++){
					if(sv[i].SearchByName(searchName)){
						sv[so_luong_sinh_vien].maintext();
						for(int i = 0; i < so_luong_sinh_vien; i++){
							
						
							found = true;
						}
						cout << "| " << left << setw(8) << i + 1;
						sv[i].output(); 
					}
					
				}
				if(!found){
					cout << "Khong tim thay sinh vien co ten chua '" << searchName << "'" << endl;
				}
				break;
			}
		}	
	}
	while(lua_chon != 10);
	

	
	return 0;
}
