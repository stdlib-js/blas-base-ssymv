<!--

@license Apache-2.0

Copyright (c) 2024 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# ssymv

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Perform the matrix-vector operation `y = α*A*x + β*y`.



<section class="usage">

## Usage

To use in Observable,

```javascript
ssymv = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-base-ssymv@umd/browser.js' )
```

To vendor stdlib functionality and avoid installing dependency trees for Node.js, you can use the UMD server build:

```javascript
var ssymv = require( 'path/to/vendor/umd/blas-base-ssymv/index.js' )
```

To include the bundle in a webpage,

```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/blas-base-ssymv@umd/browser.js"></script>
```

If no recognized module system is present, access bundle contents via the global scope:

```html
<script type="text/javascript">
(function () {
    window.ssymv;
})();
</script>
```

#### ssymv( order, uplo, N, α, A, LDA, x, sx, β, y, sy )

Performs the matrix-vector operation `y = α*A*x + β*y` where `α` and `β` are scalars, `x` and `y` are `N` element vectors, and `A` is an `N` by `N` symmetric matrix.

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 1.0, 4.0, 5.0, 4.0, 2.0, 6.0, 5.0, 6.0, 3.0 ] );
var x = new Float32Array( [ 1.0, 1.0, 1.0 ] );
var y = new Float32Array( [ 0.0, 0.0, 0.0 ] );

ssymv( 'row-major', 'lower', 3, 1.0, A, 3, x, 1, 0.0, y, 1 );
// y => <Float32Array>[ 10.0, 12.0, 14.0 ]
```

The function has the following parameters:

-   **order**: storage layout.
-   **uplo**: specifies whether the upper or lower triangular part of the symmetric matrix `A` should be referenced.
-   **N**: number of elements along each dimension of `A`.
-   **α**: scalar constant.
-   **A**: input matrix stored in linear memory as a [`Float32Array`][mdn-float32array].
-   **LDA**: stride of the first dimension of `A` (a.k.a., leading dimension of the matrix `A`).
-   **x**: input [`Float32Array`][mdn-float32array].
-   **sx**: stride length for `x`.
-   **β**: scalar constant.
-   **y**: output [`Float32Array`][mdn-float32array].
-   **sy**: stride length for `y`.

The stride parameters determine how elements in the input arrays are accessed at runtime. For example, to iterate over the elements of `x` in reverse order,

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 1.0, 4.0, 5.0, 4.0, 2.0, 6.0, 5.0, 6.0, 3.0 ] );
var x = new Float32Array( [ 1.0, 1.0, 1.0 ] );
var y = new Float32Array( [ 0.0, 0.0, 0.0 ] );

ssymv( 'row-major', 'upper', 3, 1.0, A, 3, x, -1, 1.0, y, 1 );
// y => <Float32Array>[ 10.0, 12.0, 14.0 ]
```

Note that indexing is relative to the first index. To introduce an offset, use [`typed array`][mdn-typed-array] views.

<!-- eslint-disable stdlib/capitalized-comments -->

```javascript
var Float32Array = require( '@stdlib/array-float32' );

// Initial arrays...
var x0 = new Float32Array( [ 0.0, 1.0, 1.0, 1.0 ] );
var y0 = new Float32Array( [ 0.0, 0.0, 0.0, 0.0 ] );
var A = new Float32Array( [ 1.0, 4.0, 5.0, 4.0, 2.0, 6.0, 5.0, 6.0, 3.0 ] );

// Create offset views...
var x1 = new Float32Array( x0.buffer, x0.BYTES_PER_ELEMENT*1 ); // start at 2nd element
var y1 = new Float32Array( y0.buffer, y0.BYTES_PER_ELEMENT*1 ); // start at 2nd element

ssymv( 'row-major', 'upper', 3, 1.0, A, 3, x1, -1, 1.0, y1, -1 );
// y0 => <Float32Array>[ 0.0, 14.0, 12.0, 10.0 ]
```

#### ssymv.ndarray( uplo, N, α, A, sa1, sa2, oa, x, sx, ox, β, y, sy, oy )

Performs the matrix-vector operation `y = α*A*x + β*y` using alternative indexing semantics and where `α` and `β` are scalars, `x` and `y` are `N` element vectors, and `A` is an `N` by `N` symmetric matrix.

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 1.0, 4.0, 5.0, 4.0, 2.0, 6.0, 5.0, 6.0, 3.0 ] );
var x = new Float32Array( [ 1.0, 1.0, 1.0 ] );
var y = new Float32Array( [ 0.0, 0.0, 0.0 ] );

ssymv.ndarray( 'upper', 3, 1.0, A, 3, 1, 0, x, -1, 2, 1.0, y, 1, 0 );
// y => <Float32Array>[ 10.0, 12.0, 14.0 ]
```

The function has the following additional parameters:

-   **sa1**: stride for the first dimension of `A`.
-   **sa2**: stride for the second dimension of `A`.
-   **oa**: starting index for `A`.
-   **ox**: starting index for `x`.
-   **oy**: starting index for `y`.

While [`typed array`][mdn-typed-array] views mandate a view offset based on the underlying buffer, the offset parameters support indexing semantics based on starting indices. For example,

```javascript
var Float32Array = require( '@stdlib/array-float32' );

var A = new Float32Array( [ 1.0, 4.0, 5.0, 4.0, 2.0, 6.0, 5.0, 6.0, 3.0 ] );
var x = new Float32Array( [ 1.0, 1.0, 1.0 ] );
var y = new Float32Array( [ 0.0, 0.0, 0.0 ] );

ssymv.ndarray( 'lower', 3, 1.0, A, 3, 1, 0, x, -1, 2, 1.0, y, -1, 2 );
// y => <Float32Array>[ 14.0, 12.0, 10.0 ]
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   `ssymv()` corresponds to the [BLAS][blas] level 2 function [`ssymv`][ssymv].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/random-array-discrete-uniform@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/array-ones@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/blas-base-ssymv@umd/browser.js"></script>
<script type="text/javascript">
(function () {

var opts = {
    'dtype': 'float32'
};

var N = 5;
var A = ones( N*N, opts.dtype );

var x = discreteUniform( N, 0, 255, opts );
var y = discreteUniform( N, 0, 255, opts );

ssymv( 'row-major', 'upper', N, 1.0, A, N, x, 1, 1.0, y, 1 );
console.log( y );

ssymv.ndarray( 'upper', N, 1.0, A, N, 1, 0, x, 1, 0, 1.0, y, 1, 0 );
console.log( y );

})();
</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- C interface documentation. -->



<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/blas-base-ssymv.svg
[npm-url]: https://npmjs.org/package/@stdlib/blas-base-ssymv

[test-image]: https://github.com/stdlib-js/blas-base-ssymv/actions/workflows/test.yml/badge.svg?branch=v0.1.0
[test-url]: https://github.com/stdlib-js/blas-base-ssymv/actions/workflows/test.yml?query=branch:v0.1.0

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/blas-base-ssymv/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/blas-base-ssymv?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/blas-base-ssymv.svg
[dependencies-url]: https://david-dm.org/stdlib-js/blas-base-ssymv/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/blas-base-ssymv/tree/deno
[deno-readme]: https://github.com/stdlib-js/blas-base-ssymv/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/blas-base-ssymv/tree/umd
[umd-readme]: https://github.com/stdlib-js/blas-base-ssymv/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/blas-base-ssymv/tree/esm
[esm-readme]: https://github.com/stdlib-js/blas-base-ssymv/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/blas-base-ssymv/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/blas-base-ssymv/main/LICENSE

[blas]: http://www.netlib.org/blas

[ssymv]: https://www.netlib.org/lapack/explore-html/db/d17/group__hemv_ga8990fe737209f3401522103c85016d27.html#ga8990fe737209f3401522103c85016d27

[mdn-float32array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float32Array

[mdn-typed-array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray

</section>

<!-- /.links -->
