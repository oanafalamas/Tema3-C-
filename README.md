#include<iostream>
using namespace std;

class Ciocolata
{
private:
	char* producator;
	char* denumire;
	char tip_ciocolata[50];
	unsigned int numar_ciocolata;
	double pret;
        
	
	const int id_ciocolata;
	static unsigned int numar_cutii;

public:
	Ciocolata() :id_ciocolata(Ciocolata::numar_cutii++) 
	{
		this->producator = new char[strlen("Lipsa") + 1];
		strcpy(this->producator, "Lipsa");
		this->denumire = new char[strlen("Lipsa") + 1];
		strcpy(this->denumire, "Lipsa");
		strcpy(this->tip_ciocolata, "Lipsa");
		this->numar_ciocolata = 0;
		this->pret = 0;
	
	}

	//constructor cu parametrii
	Ciocolata(char* producator, char* denumire, char tip_ciocolata[50], unsigned int numar_ciocolata, double pret) :id_ciocolata(Ciocolata::numar_cutii++)
	{
		this->producator = new char[strlen(producator) + 1];
		strcpy(this->producator, producator);

		this->denumire = new char[strlen(denumire) + 1];
		strcpy(this->denumire, denumire);

		strcpy(this->tip_ciocolata, tip_ciocolata);
		this->numar_ciocolata = numar_ciocolata;
		this->pret = pret;
		
	}

// constructor cu valori implicite 
	Ciocolata(char* producator, char* denumire, char* tip_ciocolata, unsigned int nr_ciocolata = 10) :numar_ciocolata(nr_ciocolata), id_ciocolata(Ciocolata::numar_cutii++)
	{
		this->producator = new char[strlen(producator) + 1];
		strcpy(this->producator, producator);

		this->denumire = new char[strlen(denumire) + 1];
		strcpy(this->denumire, denumire);

		strcpy(this->tip_ciocolata, tip_ciocolata);

		this->pret = 0;
	}

	//constructor de copiere
	Ciocolata(const Ciocolata& ciocolata) :id_ciocolata(ciocolata.id_ciocolata)
	{
		this->producator = new char[strlen(ciocolata.producator) + 1];
		strcpy(this->producator, ciocolata.producator);

		this->denumire = new char[strlen(ciocolata.denumire) + 1];
		strcpy(this->denumire, ciocolata.denumire);

		strcpy(this->tip_ciocolata, ciocolata.tip_ciocolata);
		this->numar_ciocolata = ciocolata.numar_ciocolata;
		this->pret = ciocolata.pret;
	}

	//supraincarcarea operatorului=
	Ciocolata& operator=(const Ciocolata& ciocolata)
	{
		if (this->producator != NULL){
			delete[] this->producator;
		}
		this->producator = new char[strlen(ciocolata.producator) + 1];
		strcpy(this->producator, ciocolata.producator);
		if (this->denumire != NULL)
		{
			delete[] this->denumire; //evit memory leaks
		}
		this->denumire = new char[strlen(ciocolata.denumire) + 1];
		strcpy(this->denumire, ciocolata.denumire);

		strcpy(this->tip_ciocolata, ciocolata.tip_ciocolata);
		this->numar_ciocolata = ciocolata.numar_ciocolata;
		this->pret = ciocolata.pret;

		return *this;
	}

	~Ciocolata()
	{
		delete[] this->producator;
		delete[] this->denumire;
	}

	void afisare();
//getter si setter

        char* getProducator()
	{
		return this->producator;
	}

	void setProducator(char* producator)
	{
		if (this->producator != NULL)
		{
			delete[] this->producator;
		}
		this->producator = new char[strlen(producator) + 1];
		strcpy(this->producator, producator);
	}
	char* getDenumire()
	{
		return this->denumire;
	}

	void setDenumire(char* denumire)
	{
		if (this->denumire != NULL)
		{
			delete[] this->denumire;
		}
		this->denumire = new char[strlen(denumire) + 1];
		strcpy(this->denumire, denumire);
	}

	unsigned int getNrCiocolata()
	{
		return this->numar_ciocolata;
	}

	void setNrCiocolata(unsigned int numar_ciocolata)
	{
		this->numar_ciocolata = numar_ciocolata;
	}
	char* getTip_ciocolata()
	{
		return this->tip_ciocolata;
	}

	void setTip_ciocolata(char tip_ciocolata[50])
	{
		strcpy(this->tip_ciocolata, tip_ciocolata);
	}


	double getPret()
	{
		return this->pret;
	}

         int getIdCiocolata()
	{
		return this->id_ciocolata;
	}

	static unsigned int getNumarCutii()
	{
		return Ciocolata::numar_cutii;
	}
};

unsigned int Ciocolata::numar_cutii = 1;

void Ciocolata::afisare()
{
	cout << "Id: " << this->id_ciocolata << endl;
	cout << "Producator: " << this->producator << endl;
	cout << "Denumire: " << this->denumire << endl;
	cout << "Tip_ciocolata: " << this->tip_ciocolata << endl;
	cout << "Numar ciocolata: " << this->numar_ciocolata << endl;
	cout << "Pret: " << this->pret << endl;
}


void main()
{
	Ciocolata ciocolata1;
	ciocolata1.afisare();

	Ciocolata ciocolata2("Belgia", "Milka", "Ciocolata Alba", 3500, 20);
	ciocolata2.afisare();

	Ciocolata ciocolata3("Franta", "Heidi", "Ciocolata neagra cu alune");
	ciocolata3.afisare();
	Ciocolata ciocolata4 = ciocolata3;//constructor de copiere
	ciocolata4.afisare();
	
	ciocolata3.setDenumire("Denumire noua");
	ciocolata3.setNrCiocolata(50);
	ciocolata3.setTip_ciocolata("Caramel");

	cout << ciocolata3.getDenumire() << endl;
	cout << ciocolata3.getNrCiocolata() << endl;
	cout << ciocolata3.getTip_ciocolata() << endl;

	Ciocolata ciocolata5;
	ciocolata5 = ciocolata2; // operatorul = 
	ciocolata5.afisare();


}
