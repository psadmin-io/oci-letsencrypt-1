# Build stage
FROM fnproject/ruby:2.7-dev as build-stage

WORKDIR /function

# Install dependencies
ADD Gemfile* /function/
RUN bundle install --path vendor/bundle

# Copy function files
ADD func.rb func.yaml models.rb /function/

# Runtime stage
FROM fnproject/ruby:2.7

WORKDIR /function
COPY --from=build-stage /function /function

ENTRYPOINT ["ruby", "func.rb"]
