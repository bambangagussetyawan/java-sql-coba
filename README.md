a.	Tes koneksi
package project;

import java.sql.*;

public class DataBase_OOP{
public Connection getConnection(){
	Connection con = null;
	String username = "root";
	String password = "";
	String dburl = "jdbc:mysql://localhost/project_oop_new";
	
	try{//Driver DatabaseMySQL
		Class.forName("com.mysql.jdbc.Driver");
		con = DriverManager.getConnection(dburl,username,password);
		}
	catch (ClassNotFoundException e) {
		e.printStackTrace();
		}
	catch(SQLException e){ 
		con =null;
		}
	if(con != null){
	System.out.println("Koneksi Berhasil Mas Bro");
	System.out.println("Alhamdulilah ");
	}else{
	System.out.println("Koneksi TIdak Berhasil");
	}
	return  con; }
	private void TextDialog() {
		System.out.println("Editing By Bambang_17111036");
		
		System.exit(0);}

public static void main(String[] args) {
	DataBase_OOP coba = new DataBase_OOP();
	coba.getConnection();
	coba.TextDialog();
	
	}
  b.	Menu
package project;

	import javax.swing.*;
	import java.awt.event.*;

	class Desain_Menu extends JFrame{
		private static final long serialVersionUID =1L;
		
		JMenuBar MenuUtama= new JMenuBar();
		JMenu	Menu= new JMenu("Menu");
		JMenuItem Legalisir=new JMenuItem("Legalisir");
		JMenuItem About = new JMenuItem("About");
		JMenuItem Keluar = new JMenuItem("Keluar");
		
		Desain_Menu(){
		setTitle("Program Menu Legalisir Universitas Mercu Buana Yogyakarta");
		setLocation(200,200);
		setSize(500,100);
		setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);
				}
		
	void Layout(){
		setJMenuBar(MenuUtama);
		MenuUtama.add(Menu);
		Menu.add(Legalisir);
		Menu.add(About);
		Menu.add(Keluar);
		setVisible(true);
	}
		
	void aksi() {
		//menu file -> about
		About.addActionListener(new ActionListener() {
		public void actionPerformed(ActionEvent e) { {                                              
			JOptionPane.showMessageDialog(null, "Universitas Mercubuana Yogyakarta \n"
					+ "Jalan Wates Km. 10, Argomulyo, Sedayu, Bantul, Daerah Istimewa Yogyakarta 55753 \n"
					+ "Phone  (0274) 6498212", "Legalisir Ijazah"
					, JOptionPane.INFORMATION_MESSAGE); 
			
		}
			}});
		
		Legalisir.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
			Data data = new Data();
			((Data)data).Posisi();
			data.Event();
						
			}
			
		});
		Keluar.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
			System.exit(0); 
			}});
		}
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Desain_Menu g=new Desain_Menu(); //konctruktor
		g.Layout();//memanggil metode 
		g.aksi(); // memanggil aksi
		g.setVisible(true);// menampilkan frame
		}	}
c.	Rekap Data Nota
package project;

import java.awt.BorderLayout;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import javax.swing.JFrame;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.table.DefaultTableModel;
import com.mysql.jdbc.ResultSetMetaData;

public class Tampilan_Isi extends JPanel { 
			/**
	 * 
	 */
	private static final long serialVersionUID = 1L;
			String[] header = {"id_Transaksi","Nama","Phone","Tanggal","Ijazah",
					"Transkrip","Akreditasi","Akta_Mengajar","Jumlah","Bayar"}; 
			JTable Nota = new JTable(); 
			JScrollPane scrollTable = new JScrollPane(); 
public Object[][] isiTable = null; 
			
	Tampilan_Isi(){ 
		DataBase_OOP open = new DataBase_OOP();
		Connection mysql = open.getConnection();
			try { 
				Statement kalimat = mysql.createStatement();
			String sql = "SELECT * FROM nota"; 
			ResultSet res = kalimat.executeQuery(sql); 
			

			ResultSetMetaData meta = (ResultSetMetaData) res.getMetaData(); 
			int kolom = meta.getColumnCount(); 
				int baris = 0; 
				while(res.next()) { 
				baris = res.getRow(); 
				} 
				
				isiTable = new Object[baris][kolom]; 
				int x = 0; 
				res.beforeFirst(); 
				while(res.next()) { 
				isiTable[x][0] = res.getString("Id_Transaksi"); 
				isiTable[x][1] = res.getString("Nama"); 
				isiTable[x][2] = res.getString("Phone");
				isiTable[x][3] = res.getString("Tanggal"); 
				isiTable[x][4] = res.getString("Ijazah"); 
				isiTable[x][5] = res.getString("Transkrip");
				isiTable[x][6] = res.getString("Akreditasi"); 
				isiTable[x][7] = res.getString("Akta_Mengajar");
				isiTable[x][8] = res.getString("Jumlah");
				isiTable[x][9] = res.getString("Bayar"); 
				
				x++; 
				} 
				scrollTable.setViewportView(Nota); 
				Nota.setModel(new DefaultTableModel(isiTable, header)); 
				add(scrollTable, BorderLayout.SOUTH); 
				kalimat.close(); 
				res.close();
						}
		catch (Exception ex){
					JOptionPane.showMessageDialog(null, "Data Mahasiswa Error");
						}
						}
	void Layout(){
					JFrame frame = new JFrame("Data Isian");
					frame.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);
					Tampilan_Isi content = new Tampilan_Isi();
					content.setOpaque(true);
					frame.setContentPane(content);
					frame.pack();
					frame.setLocationRelativeTo(null);
					frame.setVisible(true);
					}
	public static void main(String [] args){
		Tampilan_Isi b= new Tampilan_Isi();
		b.Layout();
		
	}
	}

d.	Program isian Legalisir
package project;

	
import javax.swing.JFrame;
import javax.swing.JRadioButton;
import javax.swing.JTable;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JTextField;
import javax.swing.JComboBox;
import java.awt.print.PrinterException;
import java.text.MessageFormat;
import java.util.logging.Level;
import java.util.logging.Logger;
import javax.swing.JTable.PrintMode;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import javax.swing.ButtonGroup;
import javax.swing.JButton;



public class Data extends JFrame {
	
	
	private static final long serialVersionUID = 1L;

				
	JLabel Judul = new JLabel("Selamat Datang Di Sistem Legalisir \n");
	JLabel univ = new JLabel("Universitas Mercubuana Yogyakarta \n");
	JLabel silakan = new JLabel("Silakan Isi Form Dibawah Ini \n");
	
	JLabel label_NIM = new JLabel("NIM");
	JTextField text_NIM = new JTextField (35);
	
	//membuat label name
	JLabel label_Name = new JLabel("Name");			//contruktor label nama
	JTextField text_Name = new JTextField(35);		//construktor label text nama
	
	//membuat label address
	JLabel label_Thlulus = new JLabel ("Tahun Lulus");
	JTextField text_thlulus = new JTextField (50);
	
	//membuat label Gender
	
	
	JLabel Prodi = new JLabel ("Prodi");
	String []  Prodi1= {"Teknik Informatika","Sistem Informatika","Teknik Agro Teknologi","Teknik Pengolahan Hasil Pertanian"};
	JComboBox<Object> combo_prodi=new JComboBox<Object>(Prodi1);
	
	JLabel Telpon= new JLabel ("Telepon");
	JTextField telpon1 = new JTextField();
	
	JLabel legalisir = new JLabel("Masukan Jumlah Lembar Yang Akan Dilegalisir \n");
	
	JLabel Ijazah=new JLabel("ijazah");
	JTextField text_Ijazah= new JTextField();
	
	JLabel Transkrip= new JLabel("Transkrip");
	JTextField text_Transkrip = new JTextField();
	
	JLabel Akreditasi = new JLabel ("Akreditasi");
	JTextField text_Akreditasi = new JTextField ();
	
	JLabel Akta = new JLabel("Akta Mengajar");
	JTextField text_Akta = new JTextField();
	
	JLabel Faktur = new JLabel("Faktur");
	JTextField text_Faktur = new JTextField();
		
	JLabel kirim = new JLabel("Apakah Legalisir akan dikirim ?");
	JRadioButton kirim1 = new JRadioButton ("Ya");
	JRadioButton kirim2 = new JRadioButton ("Tidak");
	ButtonGroup Check2=new ButtonGroup();
	
	JButton save =new JButton("Save");
	JButton delete = new JButton("Delete");
	JButton exit = new JButton ("Keluar");
	JButton Tagihan=new JButton("Transaksi");
	JButton Cari=new JButton("Cari");
	JButton Cetak=new JButton("Cetak Nota");
	
		
	Data(){
		
		setTitle("Form Legalisir Ijazah");
		setLocation(300,300);
		setSize(480,480);
		setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);}
		
void Posisi() {
	
		
			getContentPane().setLayout(null);
			getContentPane().add(Judul);
			Judul.setBounds(150,10,400,20);
			getContentPane().add(univ);
			univ.setBounds(145, 30, 400, 20);
			getContentPane().add(silakan);
			silakan.setBounds(165,50, 400, 20);
			
			
			
			 getContentPane().add(label_Name);
			 label_Name.setBounds(10,120,80,20);
			 getContentPane().add(text_Name);
			 text_Name.setBounds(100, 120, 150, 20);
			 
			 getContentPane().add(label_Thlulus);
			 label_Thlulus.setBounds(10, 150, 150, 20);
			 getContentPane().add(text_thlulus);
			 text_thlulus.setBounds(100, 150, 150, 20);
			 
			
			
			getContentPane().add(Prodi);
			 Prodi.setBounds(10, 180, 80, 20);
			  getContentPane().add(combo_prodi);
			combo_prodi.setBounds(100, 180, 150, 20);
			
			getContentPane().add(Telpon);
			Telpon.setBounds(10, 210, 80, 20);
			getContentPane().add(telpon1);
			telpon1.setBounds(100, 210, 150, 20);
			
			getContentPane().add(legalisir);
			legalisir.setBounds(10, 240, 400, 20);
			
			getContentPane().add(Ijazah);
			Ijazah.setBounds(10,270,80,20);
			getContentPane().add(text_Ijazah);
			text_Ijazah.setBounds(100,270,150,20);
			
			getContentPane().add(Transkrip);
			Transkrip.setBounds(10, 300,80, 20);
			getContentPane().add(text_Transkrip);
			text_Transkrip.setBounds(100, 300, 150, 20);
			
			getContentPane().add(Akreditasi);
			Akreditasi.setBounds(10,330,80,20);
			getContentPane().add(text_Akreditasi);
			text_Akreditasi.setBounds(100, 330, 150, 20);
			
			getContentPane().add(Akta);
			Akta.setBounds(10, 360, 100, 20);
			getContentPane().add(text_Akta);
			text_Akta.setBounds(100, 360, 150, 20);
			
			getContentPane().add(Faktur);
			
			getContentPane().add(text_Faktur);
			text_Faktur.setBounds(320, 300, 80, 20);
			getContentPane().add(Cari);
			Cari.setBounds(320, 330, 80, 20);
		getContentPane().add(save);
		save.setBounds(320, 120, 80, 20);
		getContentPane().add(delete);
		delete.setBounds(320,150,80,20);
		getContentPane().add(exit);
		exit.setBounds(320,180, 80, 20);
		getContentPane().add(Tagihan);
		Tagihan.setBounds(320, 210, 80, 20);
		
		getContentPane().add(Cetak);
		Cetak.setBounds(320, 240, 80, 20);

		setVisible(true);
		
		
		}
void Kosong() {
			text_Name.setText("");
			text_thlulus.setText("");
			telpon1.setText("");
			text_Ijazah.setText("");
			text_Transkrip.setText("");
			text_Akreditasi.setText("");
			text_Akta.setText("");
			text_Faktur.setText("");
			}


		
void Event(){ 
	save.addActionListener(new ActionListener(){
				public void actionPerformed(ActionEvent s) {
				DataBase_OOP open = new DataBase_OOP();
				Connection mysql = open.getConnection();
				try { String combo_prodi2=null;
				
				String pilihan = combo_prodi.getSelectedItem().toString();
				if(pilihan.equals("Teknik Informatika")){combo_prodi2="Teknik Informatika";}
				else if(pilihan.equals("Sistem Informatika")){combo_prodi2="Sistem Informatika";}
				else if(pilihan.equals("Teknik Agro Teknologi")){combo_prodi2="Teknik Agro Teknologi";}
				else if(pilihan.equals("Teknik Pengolahan Hasil Pertanian")){combo_prodi2="Teknik Pengolahan Hasil Pertanian";}
				
				Statement kalimat = mysql.createStatement();
				
				String sql = "select max(Id_Transaksi) from nota";
		        ResultSet rs = kalimat.executeQuery(sql);
		         while(rs.next()){
		             int a = rs.getInt(1);
		            text_Faktur.setText(""+Integer.toString(a+1));
		               }
				
				String sql4 = "insert into project_oop_new.telpon (Id_Transaksi,Telepon)"
					+ "values('"+text_Faktur.getText()+"',' "+telpon1.getText()+ "')";
				
				int sql2 = kalimat.executeUpdate(sql4);
				
				String sql5 = "insert into project_oop_new.prodi (Id_Transaksi,Nama,Prodi,Angkatan)"
					+ "values('"+text_Faktur.getText()+"',' "+text_Name.getText()+ " ',' " +combo_prodi2+ " ',' "+text_thlulus.getText()+ " ')";
						
				int sql3 = kalimat.executeUpdate(sql5);
			
				String sql6 = "insert into project_oop_new.legalisir (Id_Transaksi,Ijazah,Transkrip,Akreditasi,Akta_Mengajar)"
				+ "values('"+text_Faktur.getText()+"','"+text_Ijazah.getText()+"',' "+text_Transkrip.getText()+"','"+text_Akreditasi.getText()+"','"+text_Akta.getText()+ "')";
				
				int sql1 = kalimat.executeUpdate(sql6);
				
				java.util.Date dt = new java.util.Date();

				java.text.SimpleDateFormat sdf = 
				     new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
				
				String currentTime = sdf.format(dt); //tanggal otomatis sytaem              
			            			       
				String sql7 = "insert into project_oop_new.transaksi(Id_Transaksi,Date,Jumlah_Lembar,Total)"
						+ "values('"+text_Faktur.getText()+"','"+currentTime+"'"
								+ ",'"+text_Ijazah.getText()+"'+' "+text_Transkrip.getText()+"'+'"+text_Akreditasi.getText()+"'+'"+text_Akta.getText()+ "'"
										+ ",(' "+text_Ijazah.getText()+" '+' "+text_Transkrip.getText()+"'"
												+ "+'"+text_Akreditasi.getText()+"'+'"+text_Akta.getText()+ "')*2000)";
				int sql8 = kalimat.executeUpdate(sql7);
				
				String sql9 ="insert into project_oop_new.nota(Id_Transaksi,Nama,Phone,Tanggal,Ijazah,Transkrip,Akreditasi,Akta_Mengajar,Jumlah,Bayar)"
						+ "values('"+text_Faktur.getText()+"','"+text_Name.getText()+"','"+telpon1.getText()+"','"+currentTime+"','"+text_Ijazah.getText()+"',"
								+ "'"+text_Transkrip.getText()+"','"+text_Akreditasi.getText()+"','"+text_Akta.getText()+"',"
										+ "'"+text_Ijazah.getText()+"'+' "+text_Transkrip.getText()+"'+'"+text_Akreditasi.getText()+"'+'"+text_Akta.getText()+ "'"
								+ ",(' "+text_Ijazah.getText()+" '+' "+text_Transkrip.getText()+"'"
										+ "+'"+text_Akreditasi.getText()+"'+'"+text_Akta.getText()+ "')*2000)"; 
				int sql10 = kalimat.executeUpdate(sql9);
				
				if (sql2== 1 && sql3 == 1){
					JOptionPane.showMessageDialog(null,"Data Berhasil Dimasukan");
					

								}
				Kosong();// mengkosongkan nilai
						}
		catch(Exception c) {
			JOptionPane.showMessageDialog(null,"Periksa data yang Anda masukan ! "); 
			} } } );
	delete.addActionListener(new ActionListener(){
		public void actionPerformed(ActionEvent s) {
		DataBase_OOP open = new DataBase_OOP();
		Connection mysql = open.getConnection();
			try {
			Statement kalimat = mysql.createStatement();
			String sql = "delete from project_oop_new.nota "
			+"where Id_Transaksi='"+text_Faktur.getText()+"'";
			int i = kalimat.executeUpdate (sql);
			String sql2 = "delete from project_oop_new.Transaksi "
					+"where Id_Transaksi='"+text_Faktur.getText()+"'";
			int sql1 = kalimat.executeUpdate (sql2);
			String sql4 = "delete from project_oop_new.legalisir "
					+"where Id_Transaksi='"+text_Faktur.getText()+"'";
			int sql3= kalimat.executeUpdate(sql4);
			String sql6 = "delete from project_oop_new.prodi "
					+"where Id_Transaksi='"+text_Faktur.getText()+"'";
			int sql5= kalimat.executeUpdate(sql6);
			String sql8 = "delete from project_oop_new.telpon "
					+"where Id_Transaksi='"+text_Faktur.getText()+"'";
			int sql7= kalimat.executeUpdate(sql8);
			if (i == 1 && sql7==1) {
			JOptionPane.showMessageDialog(null,"Data Sudah Dihapus");
			 Kosong();// mengkosongkan nilai
			} }
			catch (Exception ex){
			JOptionPane.showMessageDialog(null, ex.getMessage());
			}
			}
			});
	Cetak.addActionListener(new ActionListener(){
		public void actionPerformed(ActionEvent s) {
		DataBase_OOP open = new DataBase_OOP();
		Connection mysql = open.getConnection();
		try {
			JTable Nota = new JTable();
			Nota.print(PrintMode.FIT_WIDTH, new MessageFormat("Nota"),null);
			} catch (PrinterException ex) {
			Logger.getLogger(Tampilan_Isi.class.getName()).log(Level.SEVERE,null, ex);
			}
			JOptionPane.showMessageDialog(null,"Data Tidak Berhasil Dicetak");
			 Kosong();// mengkosongkan nilai
			} });
	Tagihan.addActionListener(new ActionListener() {
		public void actionPerformed(ActionEvent e) {
			Tampilan_Isi T= new Tampilan_Isi();
			T.Layout();}
		
	});
	Cari.addActionListener(new ActionListener(){
		public void actionPerformed (ActionEvent e){
		String search;
		DataBase_OOP open = new DataBase_OOP ();
		Connection mysql = open.getConnection();
		try {
		search=text_Faktur.getText();
		Statement kalimat= mysql.createStatement();
		String sql = "SELECT * FROM project_oop_new.nota "
		+ "WHERE Id_Transaksi like '"+search+"'";
		ResultSet res =kalimat.executeQuery (sql);
		if(res.next()){
		text_Name.setText(res.getString(1));
		text_thlulus.setText(res.getString(2));
		telpon1.setText(res.getString(3));
		text_Ijazah.setText(res.getString(5));
		text_Transkrip.setText(res.getString(7));
		text_Akreditasi.setText(res.getString(7));
		text_Akta.setText(res.getString(8));
			}
		else{
		JOptionPane.showMessageDialog(null,"Data Sudah Ada");
		}
		}
		catch (Exception ex){
		JOptionPane.showMessageDialog(null, ex.getMessage());
		}
		}
		});
		
	exit.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				JOptionPane.showMessageDialog(null, "Apakah Anda Yakin ?", "Message"
						, JOptionPane.INFORMATION_MESSAGE); 
				System.exit(DISPOSE_ON_CLOSE);
				
			}});
	
	
	}
		
		public static void main(String[] args) {
			Data data= new Data();
			((Data)data).Posisi();
			data.Event();
			data.setVisible(true);
}}
	



}
