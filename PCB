#define F_CPU 8000000UL  // Definicja częstotliwości zegara mikrokontrolera (8 MHz)
#include <avr/io.h>
#include <util/delay.h>

uint8_t current_led = 0;  // Zmienna przechowująca indeks aktualnie sterowanej diody (od 0 do 3)

// Konfiguracja portu A
void init_ports(void) {
    // Ustawienie PA0, PA1, PA2, PA3 jako wyjścia (diody), a PA4, PA5, PA6, PA7 jako wejścia (przyciski)
    DDRA = 0x0F;  // Bity 0-3 jako wyjście (00001111), bity 4-7 jako wejście (11110000)

    // Włączenie rezystorów podciągających dla pinów PA4-PA7 (dla przycisków)
    PORTA |= (1 << PA4) | (1 << PA5) | (1 << PA6) | (1 << PA7);

    // Na początku wyłączamy wszystkie diody
    PORTA &= ~(1 << PA0);
    PORTA &= ~(1 << PA1);
    PORTA &= ~(1 << PA2);
    PORTA &= ~(1 << PA3);
}

// Funkcja zmieniająca stan diody (toggle)
void toggle_led(uint8_t pin) {
    PORTA ^= (1 << pin);  // Zmienia stan diody (jeśli była włączona, wyłącza; jeśli była wyłączona, włącza)
}

// Funkcja do przełączania na kolejną diodę
void next_led(void) {
    current_led++;  // Zwiększamy indeks diody
    if (current_led > 3) {
        current_led = 0;  // Wracamy do diody PA0, jeśli przekroczyliśmy PA3
    }
}

int main(void) {
    // Inicjalizacja portów
    init_ports();

    while (1) {
        // *** Sterowanie diodą w zależności od current_led ***
        // Przycisk PA4 włącza aktualnie wybraną diodę
        if (!(PINA & (1 << PA4))) {
            PORTA |= (1 << current_led);  // Włącz aktualną diodę
        }

        // Przycisk PA5 wyłącza aktualnie wybraną diodę
        if (!(PINA & (1 << PA5))) {
            PORTA &= ~(1 << current_led);  // Wyłącz aktualną diodę
        }

        // Przycisk PA6 zmienia stan aktualnie wybranej diody (toggle)
        if (!(PINA & (1 << PA6))) {
            _delay_ms(200);  // Krótkie opóźnienie dla debounce
            toggle_led(current_led);  // Zmień stan aktualnej diody
            while (!(PINA & (1 << PA6)));  // Czekaj, aż przycisk PA6 zostanie zwolniony
        }

        // *** Przełączanie na następną diodę (PA7) ***
        if (!(PINA & (1 << PA7))) {
            _delay_ms(200);  // Krótkie opóźnienie dla debounce
            next_led();  // Przełącz na następną diodę
            while (!(PINA & (1 << PA7)));  // Czekaj, aż przycisk PA7 zostanie zwolniony
        }
    }

    return 0;
}
