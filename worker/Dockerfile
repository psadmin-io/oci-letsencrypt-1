# Build stage
FROM fnproject/ruby:2.7-dev as build-stage

WORKDIR /function

# Install dependencies
ADD Gemfile /function/
ENV BUNDLE_SILENCE_ROOT_WARNING=1
RUN bundle config set --local path 'vendor/bundle' && \
    bundle install --jobs 4 && \
    rm -f Gemfile.lock

# Copy function files
ADD func.rb func.yaml models.rb /function/

# Runtime stage
FROM fnproject/ruby:2.7

WORKDIR /function

# Copy everything
COPY --from=build-stage /function /function

# Set gem path so ruby can find the gems
ENV GEM_PATH=/function/vendor/bundle/ruby/2.7.0

ENTRYPOINT ["ruby", "func.rb"]
