/*THIS IS BOLLYWOOD GAME which is made for fun */
/* IN this game you have to guess the name of the movie by pressing push button on the guessed letter*/

#include <LiquidCrystal.h>
int i=0;

const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
char str[10][14]={"jannat-","badlapur-","sultan-","pink-","barfi-","murder-","dangal-","bala-","housefull-","cocktail-"};
 
char te[14];
int ledState=0;
int ledPin=8;
int buttonPin=7;
int buttonStateNew;
int buttonStateOld=1;
  int atr[sizeof(te)];
  boolean p=true;
  
void setup() {
  
  lcd.begin(16, 3);
  
 Serial.begin(9600);
  pinMode(ledPin,OUTPUT);
  pinMode(buttonPin,INPUT);
   
   
   randomSeed(analogRead(0));
  
   int randNumber=random(11);
  for(i=0 ; i<14 ; i++)
{te[i]=str[randNumber][i];}
  lcd.setCursor(0, 0);
 
	  for(int i=0;i<sizeof(te);i++)
atr[i]=0;
  pri(te);
}

void pri(char te[]){
  i=0;
int j=0;
  char arr[]={'a','e','i','o','u'};
	  for( i=0;te[i]!='-';i++)
	  {
		  int c=0;
		  for( j=0;j<5;j++)
		  {
			  if(te[i]==arr[j])
			  {
				  atr[i]=1;
				  c++;
				  lcd.print(arr[j]);
                  lcd.setCursor(i+1,0);
                break;
			  }
		  }
		  if(c==0)
		  {
			  lcd.print("_");
            lcd.setCursor(i+1,0);
	  	  }
        if(te[i]=='-')
          break;
	  }
  char alpha[]={'a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z'};
  lcd.setCursor(0,1);
  
  int yoyo=0;
  while(p && yoyo<5){
    yoyo++;
    int butt=digitalRead(7);
  
    int i=0;
  butt=digitalRead(7);
  while(butt!=0)
  {
    
    for( i=0;butt!=0;i++)
    {
      butt=digitalRead(7);
      lcd.print(alpha[i]);
      lcd.setCursor(0,1);
      delay(500);
      if(i>=25)
        i=i-26;
      Serial.println(butt);
      
    }
  }
    int po=15;
    for(i=0;i<14;i++)
    {
      if(te[i]=='-')
        po=i;
      if(po>=i)
        atr[i]=1;
        
    }
    
    char h;
    if(i!=-1)
    h=alpha[i];
    else
      h=alpha[0];
    for(i=0;te[i]!='-';i++)
	  {
		  int c=0;
		  if(atr[i]>=1)
		  {
			  lcd.print(te[i]);
            lcd.setCursor(i+1,0);
		  }
		  else
		  {
		  if(te[i]==h)
		  {
			  yoyo--;
			  atr[i]=1;
			  c++;
			  lcd.print(h);
            lcd.setCursor(i+1,0);
		  }
		  for( j=0;j<5;j++)
		  {
		  	  if(te[i]==arr[j])
		  	  {
		  		  c++;
		  		  lcd.print(arr[j]);
                lcd.setCursor(i+1,0);
		  	  }
		  }
		  if(c==0)
		  {
			  lcd.print("_");
            lcd.setCursor(i+1,0);
		  }}
	  }
    int co=0;
	  for(i=0;i<sizeof(te);i++)
	  {

		  if(atr[i]==1)
		  {
			 co++;
		  }
	  }
	  if(co==sizeof(te)){
	  p=false;
  lcd.setCursor(0,0);
        for(i=0;te[i]!='-';i++)
        {lcd.print(te[i]);
         lcd.setCursor(0,i+1);
        }
        lcd.setCursor(0,i+1);
        lcd.print("congratulation");
    
    
  }

  }}

    
void loop() {
  // set the cursor to column 0, line 1
  
  
  // (note: line 1 is the second row, since counting begins with 0):
  
	   lcd.setCursor(0,1);
  // print the number of seconds since reset:
  

}
