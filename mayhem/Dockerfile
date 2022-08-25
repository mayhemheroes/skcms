# Copyright 2018 Google Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
################################################################################

FROM gcr.io/oss-fuzz-base/base-builder

# checkout all sources needed to build your project
COPY . skcms
RUN rm -rf skcms/mayhem

RUN wget -O $SRC/skcms/iccprofile_seed_corpus.zip https://storage.googleapis.com/skia-fuzzer/oss-fuzz/iccprofile_seed_corpus.zip

# current directory for build script
WORKDIR skcms

COPY mayhem/build.sh $SRC/

COPY mayhem/iccprofile.options mayhem/iccprofile.dict $SRC/skcms/
ENV FUZZING_LANGUAGE=c++ SANITIZER=address ARCHITECTURE=x86_64
RUN compile
RUN chmod +x /out/iccprofile_atf
