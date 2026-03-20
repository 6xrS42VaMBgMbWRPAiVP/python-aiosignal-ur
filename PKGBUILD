# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as
#    published by the Free Software Foundation, either version 3 of the
#    License, or (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public
#    License along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
#   Levente Polyak
#     <anthraxx[at]archlinux[dot]org>

_os="$(
  uname \
    -o)"
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_git" ]]; then
  if [[ "${_evmfs}" == "true" ]]; then
    _git="true"
  elif [[ "${_evmfs}" == "false" ]]; then
    _git="false"
  fi
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="gitlab"
fi
if [[ ! -v "_git_http" ]]; then
  _git_http="${_git_service}"
fi
if [[ ! -v "_ns" ]]; then
  _ns="aio-libs"
  # _ns="themartiancompany"
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _archive_format="zip"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
_py="python"
_pyver="$(
  "${_py}" \
    -V |
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$((
  ${_pyminver} + 1))"
_pkg=aiosignal
pkgname="${_py}-${_pkg}"
pkgver=1.3.1
_commit="2b8907dc15f976d3747a16bd65f1681ae54249a3"
pkgrel=8
_pkgdesc=(
  "List of registered"
  "asynchronous callbacks"
)
pkgdesc="${_pkgdesc[*]}"
_http="https://github.com"
url="${_http}/${_ns}/${_pkg}"
arch=(
  'any'
)
license=(
  'Apache'
)
depends=(
  "${_py}"
  "${_py}-frozenlist"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-cov"
  "${_py}-pytest-asyncio"
)

source=()
sha256sums=()
_url="${url}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${_pkg}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_offline}" == "true" ]]; then
  _url="file://${HOME}/${pkgname}"
fi
_gitlab_release_sum="SKIP"
_gitlab_release_sig_sum="SKIP"
_gitlab_sum="SKIP"
_gitlab_sig_sum="SKIP"
_github_sum="c199553ca036a44aa5e6df1bf09856bed6c3b7504628d606f282dc0540303fcf"
_github_sig_sum="991e271602181f135726ba950bf3553edbb66de84be78321792d16908b0b378a"
_bundle_sum="be0a598ebdb6ebf5246b6235684cd7dc68d2b8dddd947f7d5e6da398baba5c97"
_bundle_sig_sum="ef4d4e254c2cc60447e68307addfe7dbe4839911ac8a61036eb547c88f767533"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _sum="${_bundle_sum}"
    _sig_sum="${_bundle_sig_sum}"
    # Dvorak
    _evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _sum="${_github_sum}"
      _sig_sum="${_github_sig_sum}"
      # Truocolo
      _evmfs_ns="0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b"
    fi
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _sum="SKIP"
    _sig_sum="SKIP"
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_tag_name}" == "commit" ]]; then
      if [[ "${_git_service}" == "github" ]]; then
        _sum="${_github_sum}"
        _sig_sum="${_github_sig_sum}"
        # Truocolo
        _evmfs_ns="0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b"
      elif [[ "${_git_service}" == "gitlab" ]]; then
        _sum="${_gitlab_sum}"
        _sig_sum="${_gitlab_sig_sum}"
        # Truocolo
        _evmfs_ns="0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b"
      fi
    elif [[ "${_tag_name}" == "pkgver" ]]; then
      _sum="${_github_release_sum}"
    fi
  fi
fi
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  _src="${_evmfs_src}"
  source+=(
    "${_sig_src}"
  )
  sha256sums+=(
    "${_sig_sum}"
  )
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    _uri=""
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/archive/${_commit}.${_archive_format}"
        _sum="${_github_sum}"
      elif [[ "${_tag_name}" == "pkgver" ]]; then
        _uri="${_url}/archive/v${pkgver}/${pkgname}-${pkgver}.tar.gz"
      fi
    elif [[ "${_git_service}" == "gitlab" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
      fi
    fi
    _src="${_tarfile}::${_uri}"
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
validpgpkeys=(
  # Truocolo
  #   <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
  'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      build \
    --wheel
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  PYTHONPATH="$PWD" \
  pytest \
    -v
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m \
      "installer" \
    --destdir="${pkgdir}" \
    "dist/"*".whl"
  install \
    -Dm 644 \
    "LICENSE" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  install \
    -vDm644 \
    "CHANGES.rst" \
    "README.rst" \
    -t \
    "${pkgdir}/usr/share/doc/${pkgname}"
}

# vim: ts=2 sw=2 et:
