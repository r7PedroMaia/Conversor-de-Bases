#include <iostream>
#include <stack>
#include <string>
#include <stdexcept>

using namespace std;

// Função para converter decimal para binário
string decprabin(int decimal) {
    stack<int> binariostack;
    while (decimal > 0) {
        binariostack.push(decimal % 2);
        decimal /= 2;
    }

    string binarioResult = "";
    while (!binariostack.empty()) {
        binarioResult += to_string(binariostack.top());
        binariostack.pop();
    }

    return binarioResult;
}

// Função para converter decimal para octal
string decpraOctal(int decimal) {
    stack<int> octalStack;
    while (decimal > 0) {
        octalStack.push(decimal % 8);
        decimal /= 8;
    }

    string octalResult = "";
    while (!octalStack.empty()) {
        octalResult += to_string(octalStack.top());
        octalStack.pop();
    }

    return octalResult;
}

// Função para converter decimal para hexadecimal
string decprahexa(int decimal) {
    stack<char> hexaStack;
    while (decimal > 0) {
        int remainder = decimal % 16;
        if (remainder < 10) {
            hexaStack.push('0' + remainder);
        } else {
            hexaStack.push('A' + remainder - 10);
        }
        decimal /= 16;
    }

    string hexaResult = "";
    while (!hexaStack.empty()) {
        hexaResult += hexaStack.top();
        hexaStack.pop();
    }

    return hexaResult;
}

// Função para converter binário para decimal
int binpradec(const string& binario) {
    int decimal = 0;
    int power = 1;

    for (int i = binario.length() - 1; i >= 0; --i) {
        if (binario[i] == '1') {
            decimal += power;
        } else if (binario[i] != '0') {
            throw invalid_argument("Caracter invalido na representacao binaria.");
        }
        power *= 2;
    }

    return decimal;
}

// Função para converter octal para decimal
int octalpradec(const string& octal) {
    int decimal = 0;
    int power = 1;

    for (int i = octal.length() - 1; i >= 0; --i) {
        if (octal[i] >= '0' && octal[i] <= '7') {
            decimal += (octal[i] - '0') * power;
        } else {
            throw invalid_argument("Caracter invalido na representacao octal.");
        }
        power *= 8;
    }

    return decimal;
}

// Função para converter hexadecimal para decimal
int hexapradec(const string& hexadecimal) {
    int decimal = 0;
    int power = 1;

    for (int i = hexadecimal.length() - 1; i >= 0; --i) {
        if ((hexadecimal[i] >= '0' && hexadecimal[i] <= '9') ||
            (hexadecimal[i] >= 'A' && hexadecimal[i] <= 'F') ||
            (hexadecimal[i] >= 'a' && hexadecimal[i] <= 'f')) {
            decimal += (isdigit(hexadecimal[i]) ? (hexadecimal[i] - '0') : (toupper(hexadecimal[i]) - 'A' + 10)) * power;
        } else {
            throw invalid_argument("\nCaracter invalido na representação hexadecimal.");
        }
        power *= 16;
    }

    return decimal;
}

int main() {
    int origem, destino;
    cout << "Escolha a base de origem:" << endl;
    cout << "1. Decimal" << endl;
    cout << "2. Binario" << endl;
    cout << "3. Octal" << endl;
    cout << "4. Hexadecimal" << "\n\n";
    cin >> origem;

    string escolhida;
    cout << "\nDigite os digitos da base escolhida: ";
    cin >> escolhida;

    cout << "Escolha a base de destino:" << endl;
    cout << "1. Decimal" << endl;
    cout << "2. Binario" << endl;
    cout << "3. Octal" << endl;
    cout << "4. Hexadecimal" << "\n\n";
    cin >> destino;

    try {
        switch (origem) {
            case 1: // Decimal
                switch (destino) {
                    case 1:
                        cout << "\nDecimal: " << escolhida << endl;
                        break;
                    case 2:
                        cout << "\nBinario: " << decprabin(stoi(escolhida)) << endl;
                        break;
                    case 3:
                        cout << "\nOctal: " << decpraOctal(stoi(escolhida)) << endl;
                        break;
                    case 4:
                        cout << "\nHexadecimal: " << decprahexa(stoi(escolhida)) << endl;
                        break;
                    default:
                        cout << "\nEscolha de base de destino inválida!\n" << endl;
                        break;
                }
                break;
            case 2: // Binário
                switch (destino) {
                    case 1:
                        cout << "\nDecimal: " << binpradec(escolhida) << endl;
                        break;
                    case 2:
                        cout << "\nBinario: " << escolhida << endl;
                        break;
                    case 3:
                        cout << "\nOctal: " << decpraOctal(binpradec(escolhida)) << endl;
                        break;
                    case 4:
                        cout << "\nHexadecimal: " << decprahexa(binpradec(escolhida)) << endl;
                        break;
                    default:
                        cout << "\nEscolha de base de destino invalida!\n" << endl;
                        break;
                }
                break;
            case 3: // Octal
                switch (destino) {
                    case 1:
                        cout << "\nDecimal: " << octalpradec(escolhida) << endl;
                        break;
                    case 2:
                        cout << "\nBinario: " << decprabin(octalpradec(escolhida)) << endl;
                        break;
                    case 3:
                        cout << "\nOctal: " << escolhida << endl;
                        break;
                    case 4:
                        cout << "\nHexadecimal: " << decprahexa(octalpradec(escolhida)) << endl;
                        break;
                    default:
                        cout << "\nEscolha de base de destino invalida!\n" << endl;
                        break;
                }
                break;
            case 4: // Hexadecimal
                switch (destino) {
                    case 1:
                        cout << "\nDecimal: " << hexapradec(escolhida) << endl;
                        break;
                    case 2:
                        cout << "\nBinario: " << decprabin(hexapradec(escolhida)) << endl;
                        break;
                    case 3:
                        cout << "\nOctal: " << decpraOctal(hexapradec(escolhida)) << endl;
                        break;
                    case 4:
                        cout << "\nHexadecimal: " << escolhida << endl;
                        break;
                    default:
                        cout << "\nEscolha de base de destino invalida!\n" << endl;
                        break;
                }
                break;
            default:
                cout << "\nEscolha de base de origem invalida!\n" << endl;
                break;
        }
    } catch (const invalid_argument& e) {
        cerr << "\nErro: " << e.what() << endl;
    }

    return 0;
}
