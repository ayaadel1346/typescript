# typescript
typescript question

## what is typescript ?
1) strongly typed programming language .
2) is javascript with types , add features to js without changing it like interfaces , generics , decorators .
3) detect errors at compilation time without running code.
4) analyze code as you type
5) typescript compiler compile ts code to js code (transpilation) .

## TypeScript Config Files (tsconfig.json):
A tsconfig.json file tells the compiler how to compile your project.
```ts
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "rootDir": "src",
    "outDir": "dist",
    "strict": true
  },
  "include": ["src"]
}
```
1) rootDir-> Specifies where your TypeScript source files are located.
2) outDir -> Tells TypeScript where to put compiled .js files after transpilation..

