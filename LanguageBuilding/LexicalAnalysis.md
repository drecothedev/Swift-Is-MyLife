Lexical Analysis in Swift 

Ciao! here is a scanner class that performs lexical analysis and outputs tokens: 

```swift
//
//  Scanner.swift
//  LAng
//
//  Created by Andre jones on 5/6/26.
//
/*
Description:
Scans each character inputed within the source code and returns a set a of tokens to parse.
Responsibilities:
    - Check each character
    - Relate correct characters to eachother
    - Create a list of tokens to parse

Notes:
    - Not yet completed
    -
*/

import Foundation

class Scanner {
    // Input:
    var source: String
    // Output:
    var tokens: [Token] = []
    
    // 'start and 'current act like a sliding window for our source text.
    // When multiple characters need to be kept together after scanning we create substrings with these two pointers.
    private var current: Int = 0
    private var start: Int = 0
    
    // Tracks which line we are on for error messages.
    private var line: Int = 1
    
    private var isEnd: Bool {
        return current >= source.count
    }
    
    init(source: String) {
        self.source = source
    }
    
    
    func scanTokens() {
        while !isEnd {
            start = current
            scanToken()
        }
        return
    }
    
    
    private func scanToken() {
        let c = advance()
        switch c {
        case "(":
            addToken(type: .leftParent)
        case ")":
            addToken(type: .rightParent)
        case "{":
            addToken(type: .leftBrace)
        case "}":
            addToken(type: .rightBrace)
        case ",":
            addToken(type: .comma)
        case ".":
            addToken(type: .dot)
        case "-":
            addToken(type: .minus)
        case "+":
            addToken(type: .plus)
        case ";":
            addToken(type: .semicolon)
        case "*":
            addToken(type: .star)
        case "!":
            addToken(type: match("=") ? .bangEqual : .bang)
        case ">":
            addToken(type: match("=") ? .greaterEqual : .greater)
        case "<":
            addToken(type: match("=") ? .lessEqual : .less)
        case "=":
            addToken(type: match("=") ? .equalEqual : .equal)
        case "/":
            if match("/") {
                // A commment goes until the end of the line
                while peek() != "\n" && !isEnd {
                    let _ = advance()
                }
            } else {
                addToken(type: .slash)
            }
            break
        case " ":
            let _ = ""
        case "\r":
            let _ = ""
        case "\t":
            break
        case "\n":
            line += 1
            break
        case "\"":
            string()
            break
        default:
            if isDigit(c) {
                number()
            } else if isAlpha(c) {
                
            }
            else {
            }
            break
        }
        
    }
    
    // Advances to the next character after returning the current character.
    private func advance() -> Character {
        let idx = source.index(source.startIndex, offsetBy: current)
        current += 1
        return source[idx]
    }
    
    // Adds a token that holds no literal value. Ex: =, /, +, etc.
    private func addToken(type: TokenType) {
        addToken(type: type, literalVal: .none)
    }
    
    // Overloade function for adding literal value tokens. These are numbers and strings.
    private func addToken(type: TokenType, literalVal: LiteralValue) {
        let startIdx = source.index(source.startIndex, offsetBy: start)
        let endIdx = source.index(source.startIndex, offsetBy: current)
        let text = String(source[startIdx..<endIdx])
        let tok = Token(type: type, lexeme: text, literal: literalVal, line: line)
        print("token added: \(tok)")
        tokens.append(tok)
    }
    
    // Matches on an expected character
    private func match(_ expectectedValue: Character) -> Bool {
        if peek() != expectectedValue {
            return false
        }
        current += 1
        return true
    }
    
    // Gets the current character
    private func peek() -> Character {
        guard !isEnd else { return "\0" }
        let idx = source.index(source.startIndex, offsetBy: current)
        return source[idx]
    }
    
    
    private func string() {
        /*
        Creates a String token

        - Waits for a closing quotation mark
        - If no quotation mark is found. Error is thrown
        - Uses our sliding window technique to capture the characters within the quotation marks
         */
        
        while !match("\"") {
            _ = advance()
            guard !isEnd else {
                print("ERROR: expected '\"'.")
                return
            }
        }
        
        let startIdx = source.index(source.startIndex, offsetBy: start)
        let endIdx = source.index(source.startIndex, offsetBy: current)
        let string = String(source[startIdx..<endIdx])
        let tok = Token(type: .string, lexeme: string, literal: .string(string), line: line)
        print("string added: ", tok)
        tokens.append(tok)
    }
    
    private func isDigit(_ char: Character) -> Bool {
        return char >= "0" && char <= "9"
    }
    
    private func number() {
        while isDigit(peek()) {
            _ = advance()
        }
        
        let startIdx = source.index(source.startIndex, offsetBy: start)
        let currentIdx = source.index(source.startIndex, offsetBy: current)
        let val = source[startIdx..<currentIdx]
        tokens.append(Token(type: .number, lexeme: String(val), literal: .number(Double(val) ?? 0), line: line))
        print(val, "added")
    }
    
    private func peekNext() -> Character {
        guard current <= source.count - 1 else { return "\0" }
        
        let idx = source.index(source.startIndex, offsetBy: current + 1)
        return source[idx]
    }
    
    private func isAlpha(_ char: Character) -> Bool {
        return char >= "a" && char <= "z" || char >= "A" && char <= "Z" || char == "_"
    }
    
    private func isAlphaNumeric(_ char: Character) -> Bool {
        return isAlpha(char) || isDigit(char)
    }
}

```
