
 * interrupts.c
 *
 * Created: 27-07-2019 14:19:31
 * Author : chaithanya
 */ 
#define F_cpu  20000000
#include <avr/io.h>
#include <avr/interrupt.h>
int cliflag = 0;
int main(void)
{
	
	DDRC = 0xFF;
	DDRD = 0xFF;

	PORTD |=(1 << PIND1);
	EIMSK |= (1<<INT1); 
	EICRA |= (1<<ISC01); //falling edge generates interrupt request

    /* Replace with your application code */
    while (1) 
    {
		if (cliflag==0)
		{
			sei();
		}
		else
		{
			cli();
			cliflag=0;
        }
}
}

ISR(PCINT1_vect)
{
	PORTC |=(1<<PINC0)|(1<<PINC1);
	cliflag=1;
}
